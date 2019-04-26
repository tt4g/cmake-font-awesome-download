cmake_minimum_required(VERSION 3.4.0)

get_filename_component(FontAwesomeDownload_MODULE_PTAH "${CMAKE_CURRENT_LIST_DIR}" PATH)
set(FontAwesomeDownload_MODULE_PTAH "${FontAwesomeDownload_MODULE_PTAH}/cmake")

include("${FontAwesomeDownload_MODULE_PTAH}/FontAwesome5Download.cmake")
include(CTest)

enable_testing()

add_subdirectory(font_awesome5_web_download)
add_subdirectory(font_awesome5_desktop_download)
