cmake_minimum_required(VERSION 3.5)

set(CMAKE_SKIP_BUILD_RPATH FALSE)
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
set(CMAKE_BUILD_WITH_INSTALL_RPATH TRUE)


set(CMAKE_INSTALL_RPATH "$ORIGIN/../lib")



project(Task4)
include(ExternalProject)

enable_testing()

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${Task4_SOURCE_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${Task4_SOURCE_DIR}/lib)
set(EXTERNAL_INSTALL_LOCATION ${Task4_SOURCE_DIR}/3rdparty)

ExternalProject_Add(
    googletest_repo
    GIT_REPOSITORY https://github.com/google/googletest.git
	CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${EXTERNAL_INSTALL_LOCATION} -DCMAKE_CXX_STANDARD=${CMAKE_CXX_STANDARD}
)

add_subdirectory(${CMAKE_BINARY_DIR}/../3rdparty/$ENV{GOOGLE_TEST_DIR})

add_executable(CTest C/main_test.cpp C/tests.cpp)
target_link_libraries(CTest gtest pthread)
add_test(NAME CTest COMMAND CTest)

add_subdirectory(B)
add_subdirectory(C)

