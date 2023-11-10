set (TEST_SOURCES tests.c)
# Append additional libraries to CRITERION_LIBRARIES if they exist
if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanomsg/libnanomsg${LIB_EXT}")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanomsg/libnanomsg${LIB_EXT}")
endif()

if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanopb/libprotobuf_nanopb_static${LIB_EXT}")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanopb/libprotobuf_nanopb_static${LIB_EXT}")
endif()

if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/boxfort/src/libboxfort${LIB_EXT}")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/boxfort/src/libboxfort${LIB_EXT}")
endif()

if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/libgit2/libgit2${LIB_EXT}")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/libgit2/libgit2${LIB_EXT}")
else()
    # Execute the find program to locate libgit2${LIB_EXT}
    execute_process(
        COMMAND find "${CMAKE_BINARY_DIR}/Criterion" -name libgit2${LIB_EXT}
        OUTPUT_VARIABLE FOUND_LIBGIT2
        OUTPUT_STRIP_TRAILING_WHITESPACE
    )

    # If found, append to CRITERION_LIBRARIES
    if(FOUND_LIBGIT2)
        message(STATUS "Found libgit2${LIB_EXT} at: ${FOUND_LIBGIT2}")
        list(APPEND CRITERION_LIBRARIES "${FOUND_LIBGIT2}")
    else()
        message(WARNING "libgit2${LIB_EXT} not found in Criterion subprojects.")
    endif()
endif()


include_directories(SYSTEM "${CRITERION_INCLUDE_DIRS}")

# Add a debug message for test sources
message(STATUS "Adding executable for unit_tests with sources: ${TEST_SOURCES}")

add_executable (unit_tests "${TEST_SOURCES}")
# Add a debug message
message(STATUS "Linking unit_tests with libraries: fmem, ${CRITERION_LIBRARIES}")

target_link_libraries (unit_tests fmem "${CRITERION_LIBRARIES}")

add_test (unit_tests unit_tests)
