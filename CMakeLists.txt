cmake_minimum_required(VERSION 3.29.0)
project(planning)
set(CMAKE_CXX_STANDARD 17)

# 由于生成了动态库，而可执行文件在运行时需加载动态库
# 因此动态库需放在可执行文件同一目录（在win下分别为exe和dll）
# 指定可执行文件的生成目录
# set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
# 去掉上面的命令，改为：将动态库和exe文件都指定到bin目录
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

# 让生成的可执行文件包含刚刚创建的include和src目录
aux_source_directory(${PROJECT_SOURCE_DIR}/src SRC_LISTS)

# 把src目录下的所有cpp文件生成动态库，让planning_main.cpp生成可执行文件
# 让可执行文件连接该动态库
# （名称：common；）
add_library(common
    SHARED
    ${SRC_LISTS}
)

# 动态库依赖一些头文件，因此需包含头文件的目录
target_include_directories(common
    PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)

# 注意：runtime只用于win平台
# linux平台：CMAKE_LIBRARY_OUTPUT_DIRECTORY；静态库用：CMAKE_ARCHIVE_OUTPUT_DIRECTORY

# 生成可执行文件（依赖的文件仅planning_main.cpp）
add_executable(
    planning_main
    planning_main.cpp
)

# 可执行文件也需要包含头文件目录，通过public的方式包含目录
target_include_directories(planning_main
    PUBLIC
    ${PROJECT_SOURCE_DIR}/include
)

# 将可执行文件链接到生成的动态库上
target_link_libraries(planning_main
    PUBLIC
    common
)