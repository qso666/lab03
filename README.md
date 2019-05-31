## Homework lab03
## Задание 1
Вам поручили перейти на систему автоматизированной сборки CMake. Исходные файлы находятся в директории formatter_lib. В этой директории находятся файлы для статической библиотеки formatter. Создайте CMakeList.txt в директории formatter_lib, с помощью которого можно будет собирать статическую библиотеку formatter.
```
$ cd formatter
$ cat >> CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(formatter)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(formatter_lib1 STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter.cpp)
add_executable(formatter ${CMAKE_CURRENT_SOURCE_DIR}/formatter.cpp)
target_link_libraries(formatter formatter_lib1)
EOF
```
Проверка работы
```
$ cmake .
$ make
```
Библиотека создается. Удаляем созданное при проверке. Commit, push.
```
$ cd ..
$ git add .
$ git commit -m "Создание библиотеки formatter_lib1"
$ git push origin master
```
## Задание 2
У компании "Formatter Inc." есть перспективная библиотека, которая является расширением предыдущей библиотеки. Т.к. вы уже овладели навыком созданием CMakeList.txt для статической библиотеки formatter, ваш руководитель поручает заняться созданием CMakeList.txt для библиотеки formatter_ex, которая в свою очередь использует библиотеку formatter.
```
$ cd formatter_ex
$ cat >> CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(formatter_ex)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(formatter_exlib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex.cpp)
add_executable(formatter_ex ${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex.cpp)
target_link_libraries(formatter_ex formatter_exlib)
EOF
```
В formatter_ex.cpp нужно указать путь к файлу formatter.h
```
$ nano formatter_ex.cpp
#include "../formatter_lib/formatter.h"
```
Проверка работы. Удаление созданных файлов. Commit, push.
```
$ cmake . $ make $ cd .. $ git add . $ git commit -m "Создание библиотеки formatter_exlib" $ git push origin master
```
## Задание 3
```
Cmakelists.txt
cmake_minimum_required(VERSION 3.4) #solver_lib
project(solver_lib)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_library(solver_lib STATIC ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)
add_executable(solver ${CMAKE_CURRENT_SOURCE_DIR}/solver.cpp)
target_link_libraries(solver solver_lib)
Cmakelists.txt
cmake_minimum_required(VERSION 3.4) # solver
project(solver_app)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_executable(solver_app ${CMAKE_CURRENT_SOURCE_DIR}/equation.cpp)
Cmakelists.txt
cmake_minimum_required(VERSION 3.4) #hello_world
project(hello_world)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
add_executable(hello_world ${CMAKE_CURRENT_SOURCE_DIR}/hello_world.cpp)
```
