cmake_minimum_required(VERSION 3.10)

project(PointCloud)

find_package(Qt5 COMPONENTS Widgets Gui REQUIRED)

set(QT_USE_QTOPENGL TRUE)


find_package(OpenGL)
find_package(GLUT)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

include_directories( ./3rdparty/vcglib )

QT5_ADD_RESOURCES (RES_SRC  mainwindow.qrc )

QT5_WRAP_UI ( UI_SRC
    mainwindow.ui
    UI/normal_para.ui
    UI/para_skeletonization.ui
    UI/para_wlop.ui
    UI/upsampling_para.ui
    )

SET( APP_SRC
    calculationthread.cpp
#    Console.cpp
    DataMgr.cpp
    GLArea.cpp
    GLDrawer.cpp
    GlobalFunction.cpp
    grid.cpp
    main.cpp
    mainwindow.cpp
    Parameter.cpp
    ParameterMgr.cpp
    plylib.cpp
    trackball.cpp
    trackmode.cpp

    UI/dlg_normal_para.cpp
    UI/dlg_skeleton_para.cpp
    UI/dlg_upsampling_para.cpp
    UI/dlg_wlop_para.cpp
    UI/std_para_dlg.cpp

    Algorithm/NormalSmoother.cpp
    Algorithm/Skeleton.cpp
    Algorithm/Upsampler.cpp
    Algorithm/Skeletonization.cpp
    Algorithm/WLOP.cpp
    )

add_executable(${PROJECT_NAME} ${APP_SRC} ${RES_SRC} ${UI_SRC})


target_link_libraries(${PROJECT_NAME}
    Qt5::Widgets
    Qt5::Gui
    ${OPENGL_gl_LIBRARY}
    ${GLUT_LIBRARIES}
    glut GL GLU ann
    )
