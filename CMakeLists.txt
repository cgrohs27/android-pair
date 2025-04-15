cmake_minimum_required(VERSION 3.16)
project(android-pair LANGUAGES CXX)

find_package(Qt6 REQUIRED COMPONENTS Core Gui Widgets)

qt_standard_project_setup()

qt_add_executable(android-pair
    main.cpp
    window.cpp window.h
)

set_target_properties(android-pair PROPERTIES
    WIN32_EXECUTABLE TRUE
    MACOSX_BUNDLE TRUE
)

target_link_libraries(android-pair PRIVATE
    Qt6::Core
    Qt6::Gui
    Qt6::Widgets
)

# Resources:
set(android-pair_resource_files
    "images/android-white.png"
    "images/android-black.png"
    "images/bad.png"
    "images/heart.png"
    "images/trash.png"
)

qt_add_resources(android-pair "android-pair"
    PREFIX
        "/"
    FILES
        ${android-pair_resource_files}
)

install(TARGETS android-pair
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET android-pair
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})