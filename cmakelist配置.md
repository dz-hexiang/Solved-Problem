---
title: cmakelist配置
date: 2017-11-21 17:36:17
tags:
---

```
add_library(native-lib SHARED src/main/cpp/native-lib.cpp)
```

####  多个cpp源文件配置

```
file(GLOB helloworld_SRC "src/main/cpp/*.cpp")
add_library(testlala SHARED ${helloworld_SRC})
```

 
#### 多个cpp配置

```
add_library(testlala SHARED src/main/cpp/native-lib.cpp src/main/cpp/test.cpp)
```



#### 单个配置

```
add_library(testlala SHARED  src/main/cpp/test.cpp)
```





#### gradle 配置
 

```
   externalNativeBuild {
        cmake {
            path "CMakeLists.txt"
        }
//        ndkBuild{
//            path "src/main/cpp/Android.mk"
//
//        }
    }

android {
    compileSdkVersion 26
    buildToolsVersion "26.0.0"
    defaultConfig {
        externalNativeBuild {
            cmake {
                cppFlags "-frtti -fexceptions -std=c++11"

            }

        }
        ndk {
            stl "stlport_static"
            abiFilters "armeabi", "armeabi-v7a"
        }
	}
}
```







#### 1、 添加头文件目录，可以多引用，但是不能缺，因为缺了就编译不过

```
include_directories(
  "../../../myWindows"
  "../../../"
  "../../../include_windows"
)
```

#### 2、添加环境变量，请结合实际项目要求，不是必须的

```
add_definitions( -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_REENTRANT -DENV_UNIX -DBREAK_HANDLER -DUNICODE -D_UNICODE)

IF(APPLE)
  add_definitions(-DENV_MACOSX)
  FIND_LIBRARY(COREFOUNDATION_LIBRARY CoreFoundation )
ENDIF(APPLE)
```

#### 3、源文件

```
file(GLOB_RECURSE src_files
  "../../../../C/7zCrc.c"
  "../../../../C/7zCrcOpt.c"
  "../../../../C/7zStream.c"
  "../../../../C/Aes.c"
  "../../../../C/Alloc.c"
  "../../../../C/Bra.c"
  "../../../../C/Bra86.c"
)
```

### 4、设置生成静态库以及名称

```
add_library(myLibName STATIC ${src_files})

IF(APPLE)
   TARGET_LINK_LIBRARIES(myLibName ${COREFOUNDATION_LIBRARY} ${CMAKE_THREAD_LIBS_INIT})
ELSE(APPLE)

IF(HAVE_PTHREADS)
   TARGET_LINK_LIBRARIES(myLibName ${CMAKE_THREAD_LIBS_INIT})
  ENDIF(HAVE_PTHREADS)
ENDIF(APPLE)
```

#### CMakeLists.txt完整示例 yasea 列子

```
file(GLOB_RECURSE yuv_srcs
     "src/main/cpp/libyuv/source/compare.cc"
     "src/main/cpp/libyuv/source/compare_common.cc"
     "src/main/cpp/libyuv/source/convert.cc"
     "src/main/cpp/libyuv/source/convert_argb.cc"
     "src/main/cpp/libyuv/source/convert_from.cc"
     "src/main/cpp/libyuv/source/convert_from_argb.cc"
     "src/main/cpp/libyuv/source/convert_to_argb.cc"
     "src/main/cpp/libyuv/source/convert_to_i420.cc"
     "src/main/cpp/libyuv/source/cpu_id.cc"
     "src/main/cpp/libyuv/source/planar_functions.cc"
     "src/main/cpp/libyuv/source/rotate.cc"
     "src/main/cpp/libyuv/source/rotate_any.cc"
     "src/main/cpp/libyuv/source/rotate_argb.cc"
     "src/main/cpp/libyuv/source/rotate_common.cc"
     "src/main/cpp/libyuv/source/row_any.cc"
     "src/main/cpp/libyuv/source/row_common.cc"
     "src/main/cpp/libyuv/source/scale.cc"
     "src/main/cpp/libyuv/source/scale_any.cc "
     "src/main/cpp/libyuv/source/scale_argb.cc"
     "src/main/cpp/libyuv/source/scale_common.cc"
     "src/main/cpp/libyuv/source/video_common.cc"
)
```







