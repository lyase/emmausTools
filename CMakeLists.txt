# This is the cmake file. It describes how to build our app
# The documentation for how to build these can be found here:
#   http://www.cmake.org/cmake/help/cmake-2-8-docs.html

# CMake likes us to put this here in case someone tries to read this file with an older version of cmake
cmake_minimum_required(VERSION 2.8) # http://www.cmake.org/cmake/help/cmake-2-8-docs.html#command:cmake_minimum_required

# Sets the name of the project. Additionally this sets the variables <projectName>_BINARY_DIR and <projectName>_SOURCE_DIR to the respective values.
project ("emmaus-file-updater")      # http://www.cmake.org/cmake/help/cmake-2-8-docs.html#command:project

# Other Libraries
find_package(Boost COMPONENTS system thread signals)
find_library(wt wt)
find_library(wthttp wthttp)

# This tells cmake that we want to create an executable called 'hello' and the source files are just 'main.cpp'
add_executable(emmaus main.cpp MainWindow.cpp FileUpdaterTools.cpp fileprocessor.hpp fileprocessor.cpp)
target_link_libraries(emmaus
                      ${Boost_SYSTEM_LIBRARY} ${Boost_THREAD_LIBRARY} ${Boost_SIGNALS_LIBRARY}
                      ${wt} ${wthttp})


file(COPY run.sh debug.sh DESTINATION .)
file(COPY resources DESTINATION .)
configure_file(emmaus.xml.in emmaus.xml)
