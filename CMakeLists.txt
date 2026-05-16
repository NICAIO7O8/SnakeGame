cmake_minimum_required(VERSION 3.10)
project(SnakeGame VERSION 1.0)

# 使用 C++17 标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 设置输出目录为 bin
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
# 针对 MSVC 或某些开启 PDB 的场景，输出 pdb 到 bin 目录
set(CMAKE_PDB_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")

# 寻找 Qt 库 (兼容 Qt5/Qt6)
find_package(QT NAMES Qt6 Qt5 COMPONENTS Widgets REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets REQUIRED)

# 开启 Qt 相关的宏和代码自动生成
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC OFF) # 约束：不使用 .ui 文件
set(CMAKE_AUTORCC ON)

if(MSVC)
    add_compile_options("/utf-8")
endif()

# 收集源文件
add_executable(SnakeGame WIN32
    src/main.cpp
    src/GameEngine.h
    src/GameEngine.cpp
    src/GameWidget.h
    src/GameWidget.cpp
    src/MainWindow.h
    src/MainWindow.cpp
    res.qrc
)

# 链接 Qt 库
target_link_libraries(SnakeGame PRIVATE Qt${QT_VERSION_MAJOR}::Widgets)
