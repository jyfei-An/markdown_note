# 常见问题

## 1 dlopen | pthread 

动态库依赖pthread，使用dlopen加载动态库出现段错误

```cpp
SET(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -Wl,--no-as-needed")
target_link_libraries(test pthread dl)
```

https://github.com/belveder79/broken







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

# CPack

## IFW（跨平台的打包工具）

### 设置环境变量

QTIFWDIR=/home/jiayunfe/Qt/QtIFW-3.2.2

### Qt Installer Framework doc

https://doc.qt.io/qtinstallerframework/ifw-overview.html

### Qt Installer Framework how to use in windows

https://www.youtube.com/watch?v=1pKMcwJZay4

### Qt Installer Framework how to use in linux

https://www.youtube.com/watch?v=2B--nzfoQ9s

### linuxdeployqt

将qt的exe所需动态库拷贝到文件夹中进行打包（github上下载appimage），可参考

https://www.youtube.com/watch?v=2B--nzfoQ9s

example：

待添加

# CMake Install

## install 安装文件目录

```
install(TARGETS <target>... [...])
install({FILES | PROGRAMS} <file>... [...])
install(DIRECTORY <dir>... [...])
install(SCRIPT <file> [...])
install(CODE <code> [...])
install(EXPORT <export-name> [...])
```

## install命令参数

```
install(<FILES|PROGRAMS> files...
        TYPE <type> | DESTINATION <dir>
        [PERMISSIONS permissions...]
        [CONFIGURATIONS [Debug|Release|...]]
        [COMPONENT <component>]
        [RENAME <name>] [OPTIONAL] [EXCLUDE_FROM_ALL])
```

DESTINATION：指定磁盘上要安装文件的目录；
PERMISSIONS：指定安装文件的权限。有效权限是OWNER_READ，OWNER_WRITE，OWNER_EXECUTE，GROUP_READ，GROUP_WRITE，GROUP_EXECUTE，WORLD_READ，WORLD_WRITE，WORLD_EXECUTE，SETUID和SETGID；
CONFIGURATIONS：指定安装规则适用的构建配置列表(DEBUG或RELEASE等)；
EXCLUDE_FROM_ALL：指定该文件从完整安装中排除，仅作为特定于组件的安装的一部分进行安装；
OPTIONAL：如果要安装的文件不存在，则指定不是错误；
RENAME：指定已安装文件的名称，该名称可能与原始文件不同。仅当命令安装了单个文件时，才允许重命名。

## DESTINATION安装路径

不同的`TYPE`，`cmake`也提供了默认的安装路径

| TYPE类型 | 安装目录变量                | 默认安装文件夹 |
| -------- | --------------------------- | -------------- |
| BIN      | ${CMAKE_INSTALL_BINDIR}     | bin            |
| SBIN     | ${CMAKE_INSTALL_SBINDIR}    | sbin           |
| LIB      | ${CMAKE_INSTALL_LIBDIR}     | lib            |
| INCLUDE  | ${CMAKE_INSTALL_INCLUDEDIR} | include        |
| SYSCONF  | ${CMAKE_INSTALL_SYSCONFDIR} | etc            |
| INFO     | ${CMAKE_INSTALL_INFODIR}    | /info          |


​		

# CMake 常用命令

## 添加FPIC选项

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



## 将生成文件拷贝到指定目录

```cmake
#复制文件到执行目录
if(WIN32)
ADD_CUSTOM_COMMAND(TARGET ${CURRENT_PROJ_NAME} POST_BUILD COMMAND xcopy $(TargetPath) $(OutDir)TestDir\\Dir\\ /Y)
endif(WIN32)

if(UNIX)
#拼接字符串
string(CONCAT exename "lib" "${CURRENT_PROJ_NAME}.so")
ADD_CUSTOM_COMMAND(TARGET ${CURRENT_PROJ_NAME} POST_BUILD COMMAND cp ${CMAKE_LIBRARY_OUTPUT_DIRECTORY}/${exename}  ${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/TestDir/Dir/ )
endif(UNIX)
```

## 设置CMake最低版本

设置CMake最低版本要求

```
cmake_minimum_required(VERSION 3.12)
```

## Projects

设置项目名字

```
project (hello_cmake)
```

## Creating an Executable

编译生成可执行文件，第一个参数是可执行文件的名称，第二个参数是编译的源文件

```
add_executable(hello_cmake main.cpp)
```

## Source Files Variable

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

##  Including Directories

```
target_include_directories(target
    PRIVATE
        ${PROJECT_SOURCE_DIR}/include
)
```

## Adding a Static Library

This will be used to create a static library with the name libhello_library.a with the sources in the add_library call.

```
add_library(hello_library STATIC
    src/Hello.cpp
)
```

## Linking a Library

```
add_executable(hello_binary
    src/main.cpp
)

target_link_libraries( hello_binary
    PRIVATE
        hello_library
)
```

## Adding a Shared Library

```
add_library(hello_library SHARED
    src/Hello.cpp
)
```

## Linking a Shared Library

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

## A Basic Cmakelist.txt

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

## insatll区分windows和linux

```
if(WIN32)
  install(TARGETS ${NAME}
    RUNTIME DESTINATION path)
else()
  install(TARGETS ${NAME}
    LIBRARY DESTINATION path)
endif()   
```

## ExternalProject_Add

```
include(ExternalProject)

ExternalProject_Add(libmongoc
        GIT_REPOSITORY  "git@git.cqhorizon.com:jiayunfei/mongodb-c-driver-1.14.0.git"
        SOURCE_DIR      "${CMAKE_BINARY_DIR}/libmongoc"
        BINARY_DIR      "${CMAKE_BINARY_DIR}/libmongoc-build"
        INSTALL_DIR     "${CMAKE_BINARY_DIR}/libmongoc-install"
        CMAKE_CACHE_ARGS
            ${common_cmake_cache_args}
            -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_BINARY_DIR}/libmongoc-install
            -DENABLE_TESTS:BOOL=OFF
            -DENABLE_STATIC:BOOL=OFF
            -DENABLE_EXAMPLES:BOOL=OFF
            -DENABLE_EXTRA_ALIGNMENT:BOOL=OFF
        #INSTALL_COMMAND ""
    )
    set(libmongoc-1.0_DIR "${CMAKE_BINARY_DIR}/libmongoc-install/lib/cmake/libmongoc-1.0/")
    set(libbson-1.0_DIR "${CMAKE_BINARY_DIR}/libmongoc-install/lib/cmake/libbson-1.0/")
    
    ExternalProject_Add(libmongocxx
    GIT_REPOSITORY  "git@git.cqhorizon.com:jiayunfei/mongo-cxx-driver-r3.4.0.git"
    SOURCE_DIR      "${CMAKE_BINARY_DIR}/libmongocxx"
    BINARY_DIR      "${CMAKE_BINARY_DIR}/libmongocxx-build"
    INSTALL_DIR     "${CMAKE_BINARY_DIR}/libmongocxx-install"
    CMAKE_CACHE_ARGS
        ${common_cmake_cache_args}
        -DCMAKE_INSTALL_PREFIX:PATH=${CMAKE_BINARY_DIR}/libmongocxx-install
        -DBUILD_SHARED_LIBS:BOOL=ON
        -DENABLE_TESTS:BOOL=OFF
        -DENABLE_EXAMPLES:BOOL=OFF
        -DBSONCXX_POLY_USE_BOOST:BOOL=ON
        -DBSONCXX_POLY_USE_MNMLSTC:BOOL=OFF
        -DBSONCXX_POLY_USE_STD:BOOL=OFF
        -Dlibmongoc-1.0_DIR:PATH=${libmongoc-1.0_DIR}
        -Dlibbson-1.0_DIR:PATH=${libbson-1.0_DIR}
    DEPENDS
        libmongoc
)
set(libmongocxx_DIR "${CMAKE_BINARY_DIR}/libmongocxx-install/lib/cmake/libmongocxx-3.3.1/")
set(libbsoncxx_DIR "${CMAKE_BINARY_DIR}/libmongocxx-install//lib/cmake/libbsoncxx-3.3.1/")
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

