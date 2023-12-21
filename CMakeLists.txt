cmake_minimum_required(VERSION 3.22)
project(nfd_prj C)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK REQUIRED gtk+-3.0)


add_library(nfd STATIC ${CMAKE_CURRENT_SOURCE_DIR}/src/nfd_common.c ${CMAKE_CURRENT_SOURCE_DIR}/src/nfd_gtk.c)
target_link_libraries(nfd PUBLIC ${GTK_LIBRARIES})
target_include_directories(nfd PUBLIC ${GTK_INCLUDE_DIRS} ${CMAKE_SOURCE_DIR}/src ${CMAKE_SOURCE_DIR}/src/include)

macro(addtest test)
    add_executable(${test} test/test_${test}.c)
    target_link_libraries(${test} PUBLIC nfd)
endmacro()

addtest(opendialog)
addtest(opendialogmultiple)
addtest(pickfolder)
addtest(savedialog)
