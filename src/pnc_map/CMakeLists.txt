# 工程名
project(pnc_map)

# 将其中的cpp添加为动态库
add_library(${PROJECT_NAME}
    SHARED
    pnc_map.cpp
)

# 不需要包含其他目录以及其他库，直接生成即可
