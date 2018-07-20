CMAKE_MINIMUM_REQUIRED(VERSION 3.2)
PROJECT(qodeedit)

set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules)

SET(CMAKE_INSTALL_LIBDIR lib)
# The library output directory
SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/bin)
SET(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})

if (CMAKE_SYSTEM_NAME STREQUAL "Linux" AND CMAKE_SIZEOF_VOID_P EQUAL 8)
  SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -fPIC")
  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")
ENDIF()

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)
# Instruct CMake to run moc automatically when needed
set(CMAKE_AUTOMOC ON)
# Create code from a list of Qt designer ui files
set(CMAKE_AUTOUIC ON)

# Find the QtWidgets library
find_package(Qt5 COMPONENTS Core Widgets Xml REQUIRED)

#
#
#

SET(ABSOLUTE_DATA_DIR ${CMAKE_SOURCE_DIR}/share)
SET(VERSION "0.1.0")
configure_file(QodeEditConfig.h.in gen/QodeEditConfig.h)
include_directories(${PROJECT_BINARY_DIR}/gen)

include_directories(src)

SET(HEADERS 
    src/QodeEdit.h
    src/Tools.h
    src/editor/CodeEditor.h
    src/editor/TextDocument.h
    src/editor/PlainTextDocumentLayout.h
    src/editor/TextBlockUserData.h
    src/margin/MarginStacker.h
    src/margin/AbstractMargin.h
    src/margin/LineBookmarkMargin.h
    src/margin/LineNumberMargin.h
    src/margin/LineRevisionMargin.h
    src/margin/LineSpacingMargin.h
    src/syntax/Helpers.h
    src/syntax/List.h
    src/syntax/Document.h
    src/syntax/ItemData.h
    src/syntax/Rule.h
    src/syntax/Comment.h
    src/syntax/Keywords.h
    src/syntax/Highlighting.h
    src/syntax/Context.h
    src/syntax/General.h
    src/syntax/Folding.h
    src/syntax/EmptyLine.h
    src/syntax/Indentation.h
    src/syntax/SpellChecking.h
    src/syntax/Configuration.h
    src/syntax/Encoding.h
    src/syntax/Parser.h
    src/syntax/DocumentBuilder.h
    src/syntax/Model.h
    src/syntax/Highlighter.h
    src/syntax/ComboBox.h
    src/syntax/ContextStack.h
    src/syntax/ContextSwitcher.h
    src/theme/Theme.h
    src/Threading.h
    src/Manager.h

	${PROJECT_BINARY_DIR}/gen/QodeEditConfig.h
)

SET(SOURCES
    src/QodeEdit.cpp
    src/Tools.cpp
    src/editor/CodeEditor.cpp
    src/editor/TextDocument.cpp
    src/editor/PlainTextDocumentLayout.cpp
    src/editor/TextBlockUserData.cpp
    src/margin/MarginStacker.cpp
    src/margin/AbstractMargin.cpp
    src/margin/LineBookmarkMargin.cpp
    src/margin/LineNumberMargin.cpp
    src/margin/LineRevisionMargin.cpp
    src/margin/LineSpacingMargin.cpp
    src/syntax/Document.cpp
    src/syntax/ItemData.cpp
    src/syntax/Rule.cpp
    src/syntax/Comment.cpp
    src/syntax/Keywords.cpp
    src/syntax/Highlighting.cpp
    src/syntax/Context.cpp
    src/syntax/General.cpp
    src/syntax/Folding.cpp
    src/syntax/EmptyLine.cpp
    src/syntax/Indentation.cpp
    src/syntax/SpellChecking.cpp
    src/syntax/Configuration.cpp
    src/syntax/Encoding.cpp
    src/syntax/Parser.cpp
    src/syntax/DocumentBuilder.cpp
    src/syntax/Model.cpp
    src/syntax/Highlighter.cpp
    src/syntax/ComboBox.cpp
    src/syntax/ContextStack.cpp
    src/syntax/ContextSwitcher.cpp
    src/theme/Theme.cpp
    src/Threading.cpp
    src/Manager.cpp
)

add_library(QodeEdit STATIC ${SOURCES} ${HEADERS})

target_link_libraries(QodeEdit Qt5::Widgets Qt5::Xml)

FILE(GLOB SG_ROOT src/*.cpp src/*.h)
source_group(src FILES ${SG_ROOT})
source_group(src\\editor REGULAR_EXPRESSION editor/.*)
source_group(src\\margin REGULAR_EXPRESSION margin/.*)
source_group(src\\syntax REGULAR_EXPRESSION syntax/.*)
source_group(src\\theme REGULAR_EXPRESSION theme/.*)



add_subdirectory(example)