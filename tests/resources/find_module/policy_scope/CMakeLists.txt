cmake_minimum_required(VERSION 3.0)
project(MyApp CXX)

set(CMAKE_CXX_STANDARD 17)
find_package(hello REQUIRED)
# Request that Findbye.cmake (generated by Conan)
# is used instead of bye-config.cmake
find_package(bye MODULE REQUIRED)

# The `find_package` will include the conan_provider.cmake file
# which has policy-affecting code. We expect no changes to the current
# policy scope.

add_executable(app main.cpp)
target_link_libraries(app hello::hello bye::bye)

set(test_list a b c d e f)
if("a" IN_LIST test_list)
    # see https://cmake.org/cmake/help/latest/policy/CMP0057.html
    message(ERROR "this should not happen as IN_LIST is a CMake 3.3 feature.")
endif()