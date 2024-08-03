#  为arm平台编译libmodbus
# 1. 下载libmodbus源码

```shell
git clone https://github.com/stephane/libmodbus.git
```
# 2. 编译(x64平台)
```shell
cd libmodbus
./autogen.sh
./configure --prefix=/"自己的安装路径"
make
sudo make install
```
# 3. 交叉编译(arm平台)
```shell
cd libmodbus
./autogen.sh
./configure --host=arm-linux-gnueabihf --prefix=/"自己的安装路径"
make
sudo make install
```
# 已经编译好的libmodbus库 ./install/lib
```shell
libmodbus.so
libmodbus.so.5
libmodbus.so.5.1.0
```

# cmake使用
```cmake
cmake_minimum_required(VERSION 3.8)

project(opencv_test)

## 指定交叉编译工具链
set(CMAKE_CXX_COMPILER arm-linux-gnueabihf-g++)
set(CMAKE_C_COMPILER bin/arm-linux-gnueabihf-gcc)

# 手动指定 相关路径
include_directories(/home/sun/libmodbus/install/include/modbus)
# 指定源文件
set(SOURCE_FILES main.cpp)
#  链接libmodbus库
link_directories(/home/sun/libmodbus/install/lib/)

# 生成可执行文件
add_executable(opencv_test ${SOURCE_FILES})

# 链接OpenCV库
target_link_libraries(opencv_test modbus  )

```