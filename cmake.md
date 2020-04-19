# linux下安装打开cmkae界面

1. sudo apt-get install cmake-qt-gui
2. cmake-gui



CMake example github:

```
https://github.com/ttroy50/cmake-examples.git
```

# Directory Paths

| Variable                 | Info                                                         |
| ------------------------ | ------------------------------------------------------------ |
| CMAKE_SOURCE_DIR         | The root source directory，一般为第一个cmakelist.txt所在目录 |
| CMAKE_CURRENT_SOURCE_DIR | The current source directory if using sub-projects and directories. |
| PROJECT_SOURCE_DIR       | The source directory of the current cmake project.           |
| CMAKE_BINARY_DIR         | The root binary / build directory. This is the directory where you ran the cmake command. **一般为build输出目录** |
| CMAKE_CURRENT_BINARY_DIR | The build directory you are currently in.                    |
| PROJECT_BINARY_DIR       | The build directory for the current project.                 |

# CMake 常用命令

### Minimum CMake version

设置CMake最低版本要求

```
cmake_minimum_required(VERSION 3.12)
```

### Projects

设置项目名字

```
project (hello_cmake)
```

### Creating an Executable

编译生成可执行文件，第一个参数是可执行文件的名称，第二个参数是编译的源文件

```
add_executable(hello_cmake main.cpp)
```

### Source Files Variable

设置项目包含的源文件

```
# Create a sources variable with a link to all cpp files to compile
set(SOURCES
    src/Hello.cpp
    src/main.cpp
)

add_executable(${PROJECT_NAME} ${SOURCES})
```

使用下面这种方式也可以，但是当增加新的文件时，可能会显示不正确的结果

```
file(GLOB SOURCES "src/*.cpp")
```

###  Including Directories

```
target_include_directories(target
    PRIVATE
        ${PROJECT_SOURCE_DIR}/include
)
```

### Adding a Static Library

This will be used to create a static library with the name libhello_library.a with the sources in the add_library call.

```
add_library(hello_library STATIC
    src/Hello.cpp
)
```

### Linking a Library

```
add_executable(hello_binary
    src/main.cpp
)

target_link_libraries( hello_binary
    PRIVATE
        hello_library
)
```

### Adding a Shared Library

```
add_library(hello_library SHARED
    src/Hello.cpp
)
```

### Linking a Shared Library

```
//设置动态库的别名
add_library(hello::library ALIAS hello_library)

add_executable(hello_binary
    src/main.cpp
)

target_link_libraries(hello_binary
    PRIVATE
        hello::library
)
```

### A Basic Cmakelist.txt

```
# Set the minimum version of CMake that can be used
# To find the cmake version run
# $ cmake --version
cmake_minimum_required(VERSION 3.5)

# Set the project name
project (hello_cmake)

# Add an executable
add_executable(hello_cmake main.cpp)
```

### insatll区分windows和linux

```
if(WIN32)
  install(TARGETS ${NAME}
    RUNTIME DESTINATION path)
else()
  install(TARGETS ${NAME}
    LIBRARY DESTINATION path)
endif()   
```

### 添加FPIC选项

```
https://stackoverflow.com/questions/38296756/what-is-the-idiomatic-way-in-cmake-to-add-the-fpic-compiler-option
```

You can set the position independent code property on all targets:

```
set(CMAKE_POSITION_INDEPENDENT_CODE ON)
```

or in a specific library:

```
add_library(lib1 SHARED lib1.cpp)
set_property(TARGET lib1 PROPERTY POSITION_INDEPENDENT_CODE ON)
```

# CMake 命令行

## 设置编译模式

```
cmake -DCMAKE_BUILD_TYPE=Debug //Release, RelWithDebInfo, Debug
```

## 设置安装路径

```
//指定安装路径。UNIX 默认安装路径 /usr/local
cmake --DCMAKE_INSTALL_PREFIX=path
```

## 是否编译为动态库

```
//可以选择 ON 或者 OFF 选择默认是否编译成共享库
-DBUILD_SHARED_LIBS=ON
```

