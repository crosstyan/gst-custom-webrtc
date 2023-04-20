cmake_minimum_required(VERSION 3.11)
project(gst_uni)

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
pkg_check_modules(JSON-GLIB REQUIRED json-glib-1.0)

include_directories(${GLIB_INCLUDE_DIRS} ${GST_INCLUDE_DIRS} ${SOUP_INCLUDE_DIRS} ${JSON-GLIB_INCLUDE_DIRS})
add_executable(gst_uni unidirectional.c)

target_compile_options(gst_uni PRIVATE ${GST_CFLAGS})
target_link_libraries(gst_uni ${GLIB_LIBRARIES} ${GST_LIBRARIES} ${SOUP_LIBRARIES} ${JSON-GLIB_LIBRARIES})
