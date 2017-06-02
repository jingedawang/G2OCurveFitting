cmake_minimum_required( VERSION 2.8 )
project( G2OCurveFitting )

set( CMAKE_BUILD_TYPE "Release" )
set( CMAKE_CXX_FLAGS "-std=c++11 -O3" )

# 添加cmake模块以使用ceres库
list( APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake_modules )

# 寻找G2O
find_package( G2O REQUIRED )
include_directories(
        ${G2O_INCLUDE_DIRS}
        "/usr/include/eigen3"
)

message(STATUS "g2o include_dir ${G2O_INCLUDE_DIRS} libs ${G2O_LIBS}")

# OpenCV
find_package( OpenCV REQUIRED )
include_directories( ${OpenCV_DIRS} )

add_executable( G2OCurveFitting main.cpp )
# 与G2O和OpenCV链接
target_link_libraries( G2OCurveFitting
        ${OpenCV_LIBS}
        g2o_core g2o_stuff
        )