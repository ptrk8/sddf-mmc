
cmake_minimum_required(VERSION 3.7.2)
project(serial_test_unit CXX C)

set(CMAKE_CXX_STANDARD 11)

# These are compiler flags specific for running tests.
set(GCC_COMPILE_FLAGS -Wall -Werror -Wvla -O0 -Wno-unused-function -Wno-unused-variable)

# Download Google Test
include(FetchContent)
FetchContent_Declare(
        googletest
        # Specify the commit you depend on and update it regularly.
        URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

function(add_google_test test_target target)
    target_link_libraries(${test_target} ${target} gtest_main)
    # Using the compile flags for the main executable from GCC_COMPILE_FLAGS
    # and appending test-specific flags from GCC_COMPILE_FLAGS_TEST
    target_compile_options(${test_target} PRIVATE ${GCC_COMPILE_FLAGS} ${GCC_COMPILE_FLAGS_TEST})
    add_test(${test_target} ${test_target})
endfunction(add_google_test)


#add_executable(test_bit test_bit.cpp)
#
#add_google_test(test_bit lib_bit)

