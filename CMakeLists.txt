cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

# . 表示当前目录
aux_source_directory(. SRC_LISTS)

# 可执行文件的名称
add_executable(
    planning_main
    ${SRC_LISTS}
)