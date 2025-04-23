message(STATUS "building unit tests")
include(FetchContent)
FetchContent_Declare(
        googletest
        GIT_REPOSITORY https://github.com/google/googletest.git
        GIT_TAG        v1.16.0
)
FetchContent_MakeAvailable(googletest)
include(GoogleTest)

target_compile_definition(
        genogrove_config_version_tests
        PRIVATE
        EXPECTED_VERSION_MAJOR=${PROJECT_VERSION_MAJOR}
        EXPECTED_VERSION_MINOR=${PROJECT_VERSION_MINOR}
        EXPECTED_VERSION_PATCH=${PROJECT_VERSION_PATCH}
)

file(GLOB TEST_SOURCES *.cpp)
add_executable(genogrove_config_version_tests ${TEST_SOURCES})
target_include_directories(
        genogrove_config_version_tests
        PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/../include)
target_link_libraries(genogrove_config_version_test GTest::gtest)
gtest_discover_tests(genogrove_config_version_tests)

