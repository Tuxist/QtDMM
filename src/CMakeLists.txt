find_package(Qt5 COMPONENTS Widgets SerialPort PrintSupport REQUIRED)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

include_directories(
	${Qt5Widgets_INCLUDE_DIRS}
	${Qt5SerialPort_INCLUDE_DIRS}
	${Qt5PrintSupport_INCLUDE_DIRS}
	${CMAKE_SOURCE_DIR}/src/sources/
)

set(CMAKE_AUTOMOC ON)

set(UI_SOURCES
	forms/uiconfigdlg.ui
	forms/uidmmprefs.ui
	forms/uiexecuteprefs.ui
	forms/uigraphprefs.ui
	forms/uiguiprefs.ui
	forms/uiintegrationprefs.ui
	forms/uimainwid.ui
	forms/uimainwin.ui
	forms/uiprintdlg.ui
	forms/uirecorderprefs.ui
	forms/uiscaleprefs.ui
	forms/uitipdlg.ui
)

qt5_wrap_ui(UI_GENERATED_HEADERS ${UI_SOURCES})
qt5_add_resources(RES_SOURCES Resources.qrc)
LIST(APPEND QtDMMSRCS
	sources/colorbutton.cpp
	sources/configdlg.cpp
	sources/configitem.cpp
#	sources/displayprefs.cpp
	sources/displaywid.cpp
	sources/dmm.cpp
	sources/dmmbar.cpp
	sources/dmmgraph.cpp
	sources/dmmprefs.cpp
	sources/engnumbervalidator.cpp
	sources/executeprefs.cpp
	sources/graphprefs.cpp
	sources/guiprefs.cpp
	sources/integrationprefs.cpp
	sources/main.cpp
	sources/mainwid.cpp
	sources/mainwin.cpp
	sources/prefwidget.cpp
	sources/printdlg.cpp
	sources/readerthread.cpp
	sources/recorderprefs.cpp
	sources/scaleprefs.cpp
	sources/tipdlg.cpp
	sources/Settings.cpp
)

add_definitions(${Qt5Widgets_DEFINITIONS})

set(CMAKE_CXX_FLAGS "${Qt5Widgets_EXECUTABLE_COMPILE_FLAGS} ${CMAKE_CXX_FLAGS}")

add_executable(QtDMM
	${QtDMMSRCS} 
	${UI_GENERATED_HEADERS}
	${RES_SOURCES}
)

target_link_libraries(QtDMM 
	${Qt5Widgets_LIBRARIES} 
	${Qt5SerialPort_LIBRARIES} 
	${Qt5PrintSupport_LIBRARIES}
)

install(TARGETS QtDMM
	RUNTIME DESTINATION bin
	ARCHIVE DESTINATION lib
)