# catkin-linking-boost-library

If you are using boost library in your cpp there are several factors which you should keep in mind.

* Adjusting your `CMakeLists.txt` to have the proper link between your executable and the libraries
* Adjusting your `.cpp` 


## CMakeLists.txt

### add_definitions
In case you are working with multiple `.cpp` files instead of adding:

``` 
#define BOOST_LOG_DYN_LINK 1
  
```
in each `.cpp` file,  add the following line at the beginning of your `CMakeLists.txt`

```
add_definitions(-DBOOST_LOG_DYN_LINK=1)

```
### set CMake Flags 
Set the following Flags accordignly: 

```

set(CMAKE_BUILD_TYPE Debug)
set (CMAKE_CXX_FLAGS "-lboost_system") 
set(CMAKE_CXX_FLAGS "-lpthread")

```
### find_package 

It is required to ask CMake to find the library, you can add your prefernce components. 

```
# find_package (Boost, version, COMPONENTS ... REQUIRED)

find_package(Boost 1.54 COMPONENTS log_setup log program_options thread REQUIRED)

```

### include_directories
Make sure that the directory of the boost library is included

```
include_directories(
  include
  ${Boost_INCLUDE_DIRS}
  ${catkin_INCLUDE_DIRS}
  #....
)

```

### target link of your executable
Make sure that the library is linked to your executable 


```
add_executable(my_executable  src/file_name.cpp)


target_link_libraries(my_executble
    ${Boost_LIBRARIES}
)

```

## cpp files
Beside including the proper header files make sure to add the following line at the beginning of your cpp.

```
#define BOOST_LOG_DYN_LINK 1

```

