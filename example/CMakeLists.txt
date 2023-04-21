cmake_minimum_required(VERSION 3.11)
project(gst_my_example)

set(CMAKE_CXX_STANDARD 17)
find_package(PkgConfig REQUIRED)
pkg_search_module(GLIB REQUIRED glib-2.0)
pkg_check_modules(GST REQUIRED gstreamer-1.0
                               gstreamer-sdp-1.0
                               gstreamer-video-1.0
                               gstreamer-app-1.0
                               gstreamer-webrtc-1.0
                               gstreamer-rtp-1.0)
pkg_check_modules(SOUP REQUIRED libsoup-2.4)
pkg_check_modules(NICE REQUIRED nice)
pkg_check_modules(JSON-GLIB REQUIRED json-glib-1.0)

include_directories(${GLIB_INCLUDE_DIRS} ${GST_INCLUDE_DIRS} ${SOUP_INCLUDE_DIRS} ${JSON-GLIB_INCLUDE_DIRS} ${NICE_INCLUDE_DIRS})
set(SUPPORT_LIBRARIES ${GLIB_LIBRARIES} ${GST_LIBRARIES} ${SOUP_LIBRARIES} ${JSON-GLIB_LIBRARIES} ${NICE_LIBRARIES})

add_executable(unidirectional unidirectional.c)
target_compile_options(unidirectional PRIVATE ${GST_CFLAGS})
target_link_libraries(unidirectional ${SUPPORT_LIBRARIES})
add_executable(sendrecv sendrecv.c)
target_compile_options(sendrecv PRIVATE ${GST_CFLAGS})
# target_link_options(sendrecv PUBLIC "LINKER:-L" "LINKER:--verbose")
target_link_libraries(sendrecv ${SUPPORT_LIBRARIES})
