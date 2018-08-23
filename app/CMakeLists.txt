cmake_minimum_required(VERSION 3.4.1)

set(distribution_DIR ../../../../libs)

add_library( avcodec-58
             SHARED
             IMPORTED)
set_target_properties( avcodec-58
                       PROPERTIES IMPORTED_LOCATION
                       ${distribution_DIR}/${ANDROID_ABI}/libavcodec-58.so)


add_library(    native-lib
                SHARED
                src/main/cpp/native-lib.cpp )


find_library( log-lib
              log )



target_link_libraries(  native-lib
                        avcodec-58
                        ${log-lib} )