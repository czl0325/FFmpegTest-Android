cmake_minimum_required(VERSION 3.4.1)

set(distribution_DIR ../../../../libs)
set(CURRENT_DIR ${CMAKE_SOURCE_DIR})
message("CURRENT_DIR:" ${CMAKE_SOURCE_DIR})

add_library( avcodec-56
             SHARED
             IMPORTED)
set_target_properties( avcodec-56
                       PROPERTIES IMPORTED_LOCATION
                       ${CURRENT_DIR}/src/main/jniLibs/${ANDROID_ABI}/libavcodec-56.so)


add_library( native-lib
             SHARED
             src/main/cpp/native-lib.cpp)


find_library( log-lib
              log)

include_directories(src/main/cpp/include)

target_link_libraries(  native-lib
                        avcodec-56
                        ${log-lib})