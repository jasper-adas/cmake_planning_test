# 这里将process编译成动态库，后面将pnc_map也编译为动态库，让该动态库链接另一个
# 可执行文件又链接process动态库
# 工程名
project(process)

# 将其中的cpp添加为动态库
add_library(${PROJECT_NAME}
    SHARED
    process.cpp
)

# 指定包含目录
target_include_directories(${PROJECT_NAME}
    PUBLIC
    ${PNC_Map_Dir}
)

# 链接PNC_Map动态库
target_link_libraries(${PROJECT_NAME}
    PUBLIC
    pnc_map
)

# 包含Eigen库
target_link_libraries(${PROJECT_NAME}
    PUBLIC
    Eigen3::Eigen
)