set (TEST_SOURCES tests.c)
# Append additional libraries to CRITERION_LIBRARIES if they exist
if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanomsg/libnanomsg.a")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanomsg/libnanomsg.a")
endif()

if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanopb/libprotobuf_nanopb_static.a")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/nanopb/libprotobuf_nanopb_static.a")
endif()

if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/boxfort/src/libboxfort.a")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/boxfort/src/libboxfort.a")
endif()

if(EXISTS "${CMAKE_BINARY_DIR}/Criterion/subprojects/libgit2/src/libgit2.a")
    list(APPEND CRITERION_LIBRARIES "${CMAKE_BINARY_DIR}/Criterion/subprojects/libgit2/src/libgit2.a")
endif()


include_directories(SYSTEM "${CRITERION_INCLUDE_DIRS}")

# Add a debug message for test sources
message(STATUS "Adding executable for unit_tests with sources: ${TEST_SOURCES}")

add_executable (unit_tests "${TEST_SOURCES}")
# Add a debug message
message(STATUS "Linking unit_tests with libraries: fmem, ${CRITERION_LIBRARIES}")

target_link_libraries (unit_tests fmem "${CRITERION_LIBRARIES}")

add_test (unit_tests unit_tests)
