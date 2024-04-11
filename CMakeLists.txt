cmake_minimum_required(VERSION 3.29.0)

# 版本、描述、github链接（要将.git删除）、语言（CXX表示C++）
project(planning
    VERSION 0.0.1
    DESCRIPTION "ADAS"
    HOMEPAGE_URL "https://github.com/jasper-adas/cmake_planning_test"
    LANGUAGES CXX
)
set(CMAKE_CXX_STANDARD 17)

# 变量设置，设置动态库以及可执行文件的输出目录
# 这里设置的变量会传递到下面子目录里面，即下面子目录可用到父目录里面的变量
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

# 可以将目录放到自定义的变量中
set(Proces_Dir ${CMAKE_SOURCE_DIR}/src/process)
set(PNC_Map_Dir ${CMAKE_SOURCE_DIR}/src/pnc_map)

# 三方库
set(EIGEN3_INCLUDE_DIR "D:/library/eigen-3.4.0")

# 往变量CMAKE_MODULE_PATH增加目录"${EIGEN3_INCLUDE_DIR}/cmake"
list(APPEND CMAKE_MODULE_PATH "${EIGEN3_INCLUDE_DIR}/cmake")

# 打印
message("CMAKE_MODULE_PATH = ${CMAKE_MODULE_PATH}")

# 查找cmake文件
find_package(Eigen3 3.4 REQUIRED)

if(TARGET Eigen3::Eigen)
    message(STATUS "****** Eigen3.4 found in ${EIGEN3_INCLUDE_DIR}******")
endif()

# 添加子目录（由于该层无任何代码，直接添加子目录）该命令为找子目录里面的CMakeLists文件
add_subdirectory(src)