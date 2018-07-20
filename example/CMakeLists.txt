include_directories(../src)
include_directories(../src/editor)

SET(QICON_THEMES_PATH ${CMAKE_SOURCE_DIR}/resources/oxygen-icons-png)
configure_file(../QodeEditExampleConfig.h.in ${PROJECT_BINARY_DIR}/gen/QodeEditExampleConfig.h)

add_executable (qodeedit_example
  main.cpp
  UIMain.cpp
  UIMain.h
  UIMain.ui
)

target_link_libraries(qodeedit_example QodeEdit Qt5::Widgets Qt5::Xml)