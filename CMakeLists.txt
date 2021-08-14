################################################################################
## Basic settings
################################################################################
cmake_minimum_required(VERSION 3.21.1)

# set the project name
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# add the executable
add_executable(${PROJECT_NAME} main.cpp)

################################################################################
## Add setting for GLWF **Just change suvdirectory path **
################################################################################

set(GLFW_BUILD_DOCS OFF CACHE BOOL "GLFW lib only" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "GLFW lib only" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "GLFW lib only" FORCE)

find_package(OpenGL REQUIRED)
list(APPEND EXTRA_LIBS OpenGL::GL)

add_subdirectory(D:/Programs/glfw-master source_dir)
list(APPEND EXTRA_LIBS glfw)

################################################################################
## Add more subdirectory here - start
################################################################################

add_subdirectory(SUBDIRECTORY)
list(APPEND EXTRA_LIBS SUBDIRECTORY)


################################################################################
## Add more subdirectory here - end
################################################################################

target_link_libraries(${PROJECT_NAME} PUBLIC ${EXTRA_LIBS})

################################################################################
## Add Testing here - start
################################################################################

#[[
enable_testing()

# does the application run
add_test(NAME Runs COMMAND ${PROJECT_NAME} 25)

# does the usage message work?
add_test(NAME Usage COMMAND ${PROJECT_NAME})
set_tests_properties(Usage
        PROPERTIES PASS_REGULAR_EXPRESSION "Usage:.*number"
)

# define a function to simplify adding tests
function(do_test target arg result)
        add_test(NAME Comp_${arg} COMMAND ${target} ${arg})
        set_tests_properties(Comp_${arg}
                PROPERTIES PASS_REGULAR_EXPRESSION ${result}
        )
endfunction(do_test)

# do a bunch of result based tests
do_test(${PROJECT_NAME} 4 "4 is 2")
do_test(${PROJECT_NAME} 9 "9 is 3")
do_test(${PROJECT_NAME} 5 "5 is 2.236")
do_test(${PROJECT_NAME} 7 "7 is 2.645")
do_test(${PROJECT_NAME} 25 "25 is 5")
do_test(${PROJECT_NAME} -25 "-25 is [-nan|nan|0]")
do_test(${PROJECT_NAME} 0.0001 "0.0001 is 0.01")

################################################################################
## Add Testing here - end
################################################################################
]]