cmake_minimum_required(VERSION 3.11.0)

get_filename_component(FontAwesomeDownload_MODULE_PTAH "${CMAKE_CURRENT_LIST_DIR}" PATH)
get_filename_component(FontAwesomeDownload_MODULE_PTAH "${FontAwesomeDownload_MODULE_PTAH}" PATH)
set(FontAwesomeDownload_MODULE_PTAH "${FontAwesomeDownload_MODULE_PTAH}/cmake")

include("${FontAwesomeDownload_MODULE_PTAH}/FontAwesome5Download.cmake")
include(CTest)

enable_testing()

set(DEST_DIR "${CMAKE_BINARY_DIR}/font-awesome-5-web")

font_awesome5_web_download(
  FontAwesome5WebDownload
  OUTPUT_SOURCE_DIR FontAwesome5_WEB_SOURCE_DIR
  DOWNLOAD_VERSION 5.8.1
  DOWNLOAD_SHA256 7fbecc677a00d7dec4b99b9d213438a1e1034a73017c933af50471b6b79446a0
)

add_custom_target(CopyFontAwesome5Web ALL
  COMMAND "${CMAKE_COMMAND}" -E copy_directory "${FontAwesome5_WEB_SOURCE_DIR}" "${DEST_DIR}"
  DEPENDS FontAwesome5WebDownload
  WORKING_DIRECTORY "${FontAwesome5_WEB_SOURCE_DIR}"
  COMMENT "Copy Font-Awesome resources"
  VERBATIM
  COMMAND_EXPAND_LISTS
)

add_test(
  NAME FontAwesome5WebTestLisence
  COMMAND "${CMAKE_COMMAND}" -E compare_files "${FontAwesome5_WEB_SOURCE_DIR}/LICENSE.txt" LICENSE.txt
  WORKING_DIRECTORY "${DEST_DIR}"
)

add_test(
  NAME FontAwesome5WebTestCss
  COMMAND "${CMAKE_COMMAND}" -E compare_files "${FontAwesome5_WEB_SOURCE_DIR}/css/all.css" css/all.css
  WORKING_DIRECTORY "${DEST_DIR}"
)

add_test(
  NAME FontAwesome5WebTestJs
  COMMAND "${CMAKE_COMMAND}" -E compare_files "${FontAwesome5_WEB_SOURCE_DIR}/js/all.js" js/all.js
  WORKING_DIRECTORY "${DEST_DIR}"
)

add_test(
  NAME FontAwesome5WebTestWebFonts
  COMMAND "${CMAKE_COMMAND}" -E compare_files "${FontAwesome5_WEB_SOURCE_DIR}/webfonts/fa-brands-400.eot" webfonts/fa-brands-400.eot
  WORKING_DIRECTORY "${DEST_DIR}"
)

set_property(
  TEST FontAwesome5WebTestLisence FontAwesome5WebTestCss FontAwesome5WebTestJs FontAwesome5WebTestWebFonts
  APPEND PROPERTY
    DEPENDS CopyFontAwesome5Desktop
)
