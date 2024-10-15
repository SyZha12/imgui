cmake_minimum_required(VERSION 3.28)
project(imgui-docking)

add_library(${PROJECT_NAME} "")
#[Give the library the alias CaelumRex::CaelumRex for the target_link_libraries]
add_library(IMGUIDOCK::IMGUIDOCK ALIAS ${PROJECT_NAME})

#[This code is used for the include and src directories of the CaelumRex files]
#[[
target_include_directories(
        ${PROJECT_NAME} PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}>
        $<INSTALL_INTERFACE:include>
)
]]

set(FILES 
  ${CMAKE_CURRENT_SOURCE_DIR}/imconfig.h
  ${CMAKE_CURRENT_SOURCE_DIR}/imgui.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/imgui.h
  ${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/imgui_internal.h
  ${CMAKE_CURRENT_SOURCE_DIR}/imgui_tables.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/imgui_widgets.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/imstb_rectpack.h
  ${CMAKE_CURRENT_SOURCE_DIR}/imstb_textedit.h
  ${CMAKE_CURRENT_SOURCE_DIR}/imstb_truetype.h
)
set(SUBDIRECTORIES "")
set(RELATIVE_PATH "imgui")

#[Add all subdirectories]
foreach(VAR ${SUBDIRECTORIES})
    add_subdirectory(${VAR})
endforeach()

if(FILES)
    #[Add source files to target]
    target_sources(${PROJECT_NAME} PRIVATE ${FILES})
    #[Install source files]
    install(FILES ${FILES} DESTINATION ${RELATIVE_PATH})
endif()
