include(FetchContent)

FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG        v1.17.0
    GIT_SHALLOW    TRUE
)
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
set(INSTALL_GTEST OFF CACHE BOOL "" FORCE)
set(BUILD_GMOCK OFF CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

add_executable(pricer_tests
    test_smoke.cpp
)
target_link_libraries(pricer_tests PRIVATE
    GTest::gtest_main
    pricer_warnings
)

include(GoogleTest)
gtest_discover_tests(pricer_tests)
