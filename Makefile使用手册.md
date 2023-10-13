### Makefile使用手册--整理写在一个文件中的项目

* 编译并链接

```
g++ 文件1.cpp 文件2.cpp 文件3.cpp -o 目标
```

* 只编译不链接

```
g++ 文件1.cpp -c
```

* 将所有编译的.o文件链接到一起

```
g++ *.o -o 目标
```

> -o 后面必须跟的是目标



**将上面分散的命令整合到一个脚本文件里面就是Makefile文件**

> :后面是依赖，缺少某一个依赖时，就会去执行相应的命令来生成依赖

* 版本一：编译的时候只编译修改过的.cpp文件

```makefile
CXX = g++
TARGET = hello 
OBJ = file1.o file2.o file3.o

$(TARGET): $(OBJ)
	$(CXX) -o $(TARGET) $(OBJ)
	
file1.o: file1.cpp
	$(CXX) -c file1.cpp
	
file2.o: file2.cpp
	$(CXX) -c file2.cpp
	
file3.o: file3.cpp
	$(CXX) -c file3.cpp
```



* 版本二：在版本一的基础上加入编译选项和删除产生的中间文件

```makefile
CXX = g++
CXXFLAGS = -c -Wall
TARGET = hello
OBJ = file1.o file2.o file3.o

$(TARGET): $(OBJ)
	$(CXX) $(OBJ) -o $(TARGET)

file1.o: file1.cpp
	$(CXX) $(CXXFLAGS) file1.cpp

file2.o: file2.cpp
	$(CXX) $(CXXFLAGS) file2.cpp

file3.o: file3.cpp
	$(CXX) $(CXXFLAGS) file3.cpp

.PHONY: clean # 防止有一个叫clean的文件存在而不会执行删除命令
clean:
	rm -f *.o $(TARGET)
```



* 版本三：优化版本二，减少编译冗余

```makefile
file1.o: file1.cpp
	$(CXX) $(CXXFLAGS) file1.cpp

file2.o: file2.cpp
	$(CXX) $(CXXFLAGS) file2.cpp

file3.o: file3.cpp
	$(CXX) $(CXXFLAGS) file3.cpp
# 可以替换成如下的形式
%.o: %.cpp
	$(CXX) $(CXXFLAGS) $< -o $@
```

```makefile
$(TARGET): $(OBJ)
	$(CXX) $(OBJ) -o $(TARGET)
# 可以替换成如下的形式
$(TARGET): $(OBJ)
	$(CXX) $^ -o $@
```



* 版本四：优化版本三，在增加新的file.cpp文件时甚至不需要修改Makefile文件

```makefile
OBJ = file1.o file2.o file3.o
# 可以替换成如下的形式
SRC = $(wildcard *.cpp)
OBJ = $(patsubst %.cpp, %.o, $(SRC))
```



**通过写cmake文件来避免写复杂的Makefile文件并实现跨平台的统一（因为不同的操作系统需要不同的Makefile文件）**

```cmake
cmake_minimum_required(VERSION 3.10)

project(hello)

add_executable(hello file1.cpp file2.cpp file3.cpp)
```

运行方式：`cmake .`

运行完成之后会生成适合本操作系统的Makefile文件

由于运行该命令之后会生成很多的临时文件，因此可以新建立一个目录，把生成的临时文件都放入该目录中，方便后续的删除

```
mkdir bulid
cd build
cmake .. # 在上一层目录中去找CMakelists.txt文件
c
rm -rf build
```



> 头文件保护的目的是防止同一个头文件被多次包含，避免重复定义导致的编译错误
>
> \#ifndef EQOPT_GRAPH_HPP
>
> #define EQOPT_GRAPH_HPP
>
> #endif // EQOPT_GRAPH_HPP