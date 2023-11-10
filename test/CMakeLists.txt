set (TEST_SOURCES tests.c)
file(GLOB ALL_LIB_A_FILES "${CMAKE_BINARY_DIR}/Criterion/subprojects/*/src/*.a")
message(STATUS "Found .a files: ${ALL_LIB_A_FILES}")

include_directories(SYSTEM "${CRITERION_INCLUDE_DIRS}" "${ALL_LIB_A_FILES}")

# Add a debug message for test sources
message(STATUS "Adding executable for unit_tests with sources: ${TEST_SOURCES}")

add_executable (unit_tests "${TEST_SOURCES}")
# Add a debug message
message(STATUS "Linking unit_tests with libraries: fmem, ${CRITERION_LIBRARIES}")

target_link_libraries (unit_tests fmem "${CRITERION_LIBRARIES}")

add_test (unit_tests unit_tests)
