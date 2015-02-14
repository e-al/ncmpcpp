project(ncmpcpp)
cmake_minimum_required(VERSION 2.8)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -W -Wall")
set(CMAKE_SHARED_LINKER_FLAGS "-static-libstdc++ -static-libgcc")

link_directories(/usr/lib /usr/local/lib)

find_package(Boost COMPONENTS system filesystem program_options regex thread locale REQUIRED)
include_directories($(PROJECT_SOURCE_DIR))
include_directories(src)
include_directories(SYSTEM /usr/include /usr/include/taglib /usr/include/mpd /usr/include/curl /usr/include/readline)
#include_directories(${Boost_INCLUDE_DIRS})

file(GLOB_RECURSE NCMPCPP_SOURCES "src/*.cpp")
file(GLOB_RECURSE NCMPCPP_HEADERS "src/*.h")

add_executable(ncmpcpp ${NCMPCPP_SOURCES} ${NCMPCPP_HEADERS})

set(LIBS pthread ncurses readline curl tag mpdclient ${Boost_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${LIBS})
