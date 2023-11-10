set (TEST_SOURCES tests.c)

if(NOT CRITERION_FOUND)
    include_directories("${CRITERION_INCLUDE_DIRS}")
else()
    include_directories(SYSTEM ${CRITERION_INCLUDE_DIRS})
endif()

add_executable (unit_tests ${TEST_SOURCES})
target_link_libraries (unit_tests fmem ${CRITERION_LIBRARIES})

add_test (unit_tests unit_tests)
