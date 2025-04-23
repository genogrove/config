message(STATUS "building unit tests")
include(FetchContent)
FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG        v1.16.0
)
FetchContent_MakeAvailable(googletest)
include(GoogleTest)

# gather all test sources
file(GLOB TEST_SOURCES *.cpp)

# create the test executable
add_executable(genogrove_config_version_tests ${TEST_SOURCES})

# add include paths
target_include_directories(
        genogrove_config_version_tests
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/../include
        ${CMAKE_CURRENT_BINARY_DIR}/../include # important as we configure the version in build tree
)

# link against gtest and gtest_main
target_link_libraries(genogrove_config_version_tests GTest::gtest GTest::gtest_main)

# set the expected version definitions
target_compile_definitions(
        genogrove_config_version_tests
        PRIVATE
        EXPECTED_VERSION_MAJOR=${PROJECT_VERSION_MAJOR}
        EXPECTED_VERSION_MINOR=${PROJECT_VERSION_MINOR}
        EXPECTED_VERSION_PATCH=${PROJECT_VERSION_PATCH}
)

gtest_discover_tests(genogrove_config_version_tests)
