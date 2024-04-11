# 工程名
project(planning_main)

# 添加两个子目录
add_subdirectory(pnc_map)
add_subdirectory(process)

# 将该层的planning_main.cpp添加为可执行文件，文件名直接用工程名
add_executable(${PROJECT_NAME} planning_main.cpp)

# 添加头文件和依赖
# 首先让可执行文件以Public的方式包含process(调用自定义的变量)
target_include_directories(${PROJECT_NAME}
    PUBLIC
    ${Proces_Dir}
)

# 链接动态库
target_link_libraries(${PROJECT_NAME}
    PUBLIC
    process
)