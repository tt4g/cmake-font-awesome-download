cmake_minimum_required(VERSION 3.11.0)

get_filename_component(FontAwesomeDownload_MODULE_PTAH "${CMAKE_CURRENT_LIST_DIR}" PATH)
get_filename_component(FontAwesomeDownload_MODULE_PTAH "${FontAwesomeDownload_MODULE_PTAH}" PATH)
set(FontAwesomeDownload_MODULE_PTAH "${FontAwesomeDownload_MODULE_PTAH}/cmake")

include("${FontAwesomeDownload_MODULE_PTAH}/FontAwesome5Download.cmake")
include(CTest)

enable_testing()

set(DEST_DIR "${CMAKE_BINARY_DIR}/font-awesome-5-desktop")

font_awesome5_desktop_download(
  FontAwesome5DesktopDownload
  OUTPUT_SOURCE_DIR FontAwesome5_DESKTOP_SOURCE_DIR
  DOWNLOAD_VERSION 5.8.1
  DOWNLOAD_SHA256 888f7ff14cfbd31d4ae1e59a65f1037ed0c5460ba2a9480cda1d7d454ed31e16
)

add_custom_target(CopyFontAwesome5Desktop ALL
  COMMAND "${CMAKE_COMMAND}" -E make_directory "${DEST_DIR}/svgs"
  COMMAND "${CMAKE_COMMAND}" -E copy "${FontAwesome5_DESKTOP_SOURCE_DIR}/LICENSE.txt" "${DEST_DIR}"
  COMMAND "${CMAKE_COMMAND}" -E copy "${FontAwesome5_DESKTOP_SOURCE_DIR}/svgs/brands/500px.svg" "${DEST_DIR}/svgs"
  DEPENDS FontAwesome5DesktopDownload
  WORKING_DIRECTORY "${FontAwesome5_DESKTOP_SOURCE_DIR}"
  COMMENT "Copy Font-Awesome resources"
  VERBATIM
  COMMAND_EXPAND_LISTS
)

add_test(
  NAME FontAwesome5DesktopTestLisence
  COMMAND "${CMAKE_COMMAND}" -E compare_files "${FontAwesome5_DESKTOP_SOURCE_DIR}/LICENSE.txt" LICENSE.txt
  WORKING_DIRECTORY "${DEST_DIR}"
)
add_test(
  NAME FontAwesome5DesktopTestSvg
  COMMAND "${CMAKE_COMMAND}" -E compare_files "${FontAwesome5_DESKTOP_SOURCE_DIR}/svgs/brands/500px.svg" svgs/500px.svg
  WORKING_DIRECTORY "${DEST_DIR}"
)
set_property(
  TEST FontAwesome5DesktopTestLisence FontAwesome5DesktopTestSvg
  APPEND PROPERTY
    DEPENDS CopyFontAwesome5Desktop
)
