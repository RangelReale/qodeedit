include_directories(../src)
include_directories(../src/editor)

add_executable (qodeedit_example
  main.cpp
  UIMain.cpp
  UIMain.h
  UIMain.ui
)

target_link_libraries(qodeedit_example QodeEdit Qt5::Widgets Qt5::Xml)