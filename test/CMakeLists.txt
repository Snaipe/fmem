set (TEST_SOURCES tests.c)

add_executable (unit_tests ${TEST_SOURCES})
target_link_libraries (unit_tests fmem ${CRITERION_LIBRARIES})

add_test (unit_tests unit_tests)
