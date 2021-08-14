add_library(SUBDIRECTORY bonus.cpp bonus.hpp)

target_include_directories(SUBDIRECTORY
          INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
          )