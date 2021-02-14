#****************************************************************************
#* Copyright (c) 2021, Fougue Ltd. <http://www.fougue.pro>
#* All rights reserved.
#* See license at https://github.com/fougue/mayo/blob/master/LICENSE.txt
#****************************************************************************

cmake_minimum_required(VERSION 3.5)
project(
  mayo
  VERSION 0.4.0
  LANGUAGES CXX
)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# message(DEBUG "CMAKE_CXX_COMPILE_FEATURES = "${CMAKE_CXX_COMPILE_FEATURES})

if (NOT ${CMAKE_SYSTEM_NAME} STREQUAL "Linux")
  message(FATAL_ERROR "CMake script is only available for Linux")
endif()

find_package(OpenCASCADE 7.5.0 REQUIRED)

# FIXME Configure src/app/version.h.in, use git commit
# http://cmake.3232098.n2.nabble.com/Putting-the-git-commit-hash-in-a-cmake-variable-td7598423.html

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
find_package(Qt5 COMPONENTS Widgets REQUIRED)

# FIXME Handle translations
find_package(Qt5LinguistTools REQUIRED)

qt5_create_translation(
  QM_FILES
  src/
  i18n/mayo_en.ts
  i18n/mayo_fr.ts
)

# FIXME Variables must be set using git
set(MAYO_VERSION "abcdef")
set(MAYO_VERSION_COMMIT "abcdef")
set(MAYO_VERSION_REVNUM "643")
configure_file(
  src/app/version.h.in
  version.h
  @ONLY
)

# FIXME Taken from Qt example
add_executable(
  ${PROJECT_NAME}

  src/base/application.h
  src/base/application_item.h
  src/base/application_item_selection_model.h
  src/base/application_ptr.h
  src/base/bnd_utils.h
  src/base/brep_utils.h
  src/base/caf_utils.h
  src/base/cpp_utils.h
  src/base/document.h
  src/base/document_ptr.h
  src/base/document_tree_node.h
  src/base/document_tree_node_properties_provider.h
  src/base/enumeration_fromenum.h
  src/base/enumeration.h
  src/base/geom_utils.h
  src/base/io_format.h
  src/base/io_parameters_provider.h
  src/base/io_reader.h
  src/base/io_system.h
  src/base/io_writer.h
  src/base/libtree.h
  src/base/math_utils.h
  src/base/mesh_utils.h
  src/base/messenger.h
  src/base/meta_enum.h
  src/base/occ_progress_indicator.h
  src/base/occ_static_variables_rollback.h
  src/base/occt_enums.h
  src/base/property_builtins.h
  src/base/property_enumeration.h
  src/base/property.h
  src/base/qmeta_gp_pnt.h
  src/base/qmeta_gp_trsf.h
  src/base/qmeta_quantity_color.h
  src/base/qmeta_quantity.h
  src/base/qmeta_tdf_label.h
  src/base/qtcore_hfuncs.h
  src/base/qtcore_utils.h
  src/base/quantity.h
  src/base/result.h
  src/base/scope_import.h
  src/base/settings.h
  src/base/settings_index.h
  src/base/span.h
  src/base/string_utils.h
  src/base/task_common.h
  src/base/task.h
  src/base/task_manager.h
  src/base/task_progress.h
  src/base/text_id.h
  src/base/tkernel_utils.h
  src/base/typed_scalar.h
  src/base/unit.h
  src/base/unit_system.h
  src/base/xcaf.h

  src/io_occ/io_occ_base_mesh.h
  src/io_occ/io_occ_brep.h
  src/io_occ/io_occ_caf.h
  src/io_occ/io_occ_common.h
  src/io_occ/io_occ_gltf_reader.h
  src/io_occ/io_occ_gltf_writer.h
  src/io_occ/io_occ.h
  src/io_occ/io_occ_iges.h
  src/io_occ/io_occ_obj.h
  src/io_occ/io_occ_step.h
  src/io_occ/io_occ_stl.h
  src/io_occ/io_occ_vrml.h

  src/graphics/ais_text.h
  src/graphics/graphics_mesh_data_source.h
  src/graphics/graphics_object_base_property_group.h
  src/graphics/graphics_object_driver.h
  src/graphics/graphics_object_driver_table.h
  src/graphics/graphics_object_ptr.h
  src/graphics/graphics_owner_ptr.h
  src/graphics/graphics_scene.h
  src/graphics/graphics_tree_node_mapping_driver.h
  src/graphics/graphics_tree_node_mapping_driver_table.h
  src/graphics/graphics_tree_node_mapping.h
  src/graphics/graphics_utils.h
  src/graphics/v3d_view_camera_animation.h
  src/graphics/v3d_view_controller.h

  src/gui/gui_application.h
  src/gui/gui_document.h
  src/gui/gui_document_list_model.h
  src/gui/qtgui_utils.h

  src/app/app_module.h
  src/app/button_flat.h
  src/app/dialog_about.h
  src/app/dialog_inspect_xde.h
  src/app/dialog_options.h
  src/app/dialog_save_image_view.h
  src/app/dialog_task_manager.h
  src/app/document_tree_node_properties_providers.h
  src/app/grid_helper.h
  src/app/item_view_buttons.h
  src/app/list_helper.h
  src/app/mainwindow.h
  src/app/occt_window_740.h
  src/app/occt_window_750.h
  src/app/occt_window.h
  src/app/property_editor_factory.h
  src/app/property_item_delegate.h
  src/app/proxy_styled_item_delegate.h
  src/app/recent_files.h
  src/app/theme.h
  src/app/widget_clip_planes.h
  src/app/widget_file_system.h
  src/app/widget_gui_document.h
  src/app/widget_home_files.h
  src/app/widget_message_indicator.h
  src/app/widget_model_tree_builder.h
  src/app/widget_model_tree_builder_mesh.h
  src/app/widget_model_tree_builder_xde.h
  src/app/widget_model_tree.h
  src/app/widget_occ_view_controller.h
  src/app/widget_occ_view.h
  src/app/widget_properties_editor.h
  src/app/widget_shape_selector.h
  src/app/widgets_utils.h

  src/base/application.cpp
  src/base/application_item.cpp
  src/base/application_item_selection_model.cpp
  src/base/bnd_utils.cpp
  src/base/brep_utils.cpp
  src/base/caf_utils.cpp
  src/base/document.cpp
  src/base/document_tree_node.cpp
  src/base/document_tree_node_properties_provider.cpp
  src/base/enumeration.cpp
  src/base/geom_utils.cpp
  src/base/io_format.cpp
  src/base/io_system.cpp
  src/base/math_utils.cpp
  src/base/mesh_utils.cpp
  src/base/messenger.cpp
  src/base/occ_progress_indicator.cpp
  src/base/occ_static_variables_rollback.cpp
  src/base/occt_enums.cpp
  src/base/property_builtins.cpp
  src/base/property.cpp
  src/base/property_enumeration.cpp
  src/base/qmeta_quantity_color.cpp
  src/base/quantity.cpp
  src/base/result.cpp
  src/base/scope_import.cpp
  src/base/settings.cpp
  src/base/string_utils.cpp
  src/base/task.cpp
  src/base/task_manager.cpp
  src/base/task_progress.cpp
  src/base/text_id.cpp
  src/base/tkernel_utils.cpp
  src/base/unit.cpp
  src/base/unit_system.cpp
  src/base/xcaf.cpp

  src/io_occ/io_occ_base_mesh.cpp
  src/io_occ/io_occ_brep.cpp
  src/io_occ/io_occ_caf.cpp
  src/io_occ/io_occ_common.cpp
  src/io_occ/io_occ.cpp
  src/io_occ/io_occ_gltf_reader.cpp
  src/io_occ/io_occ_gltf_writer.cpp
  src/io_occ/io_occ_iges.cpp
  src/io_occ/io_occ_obj.cpp
  src/io_occ/io_occ_step.cpp
  src/io_occ/io_occ_stl.cpp
  src/io_occ/io_occ_vrml.cpp

  src/graphics/ais_text.cpp
  src/graphics/graphics_mesh_data_source.cpp
  src/graphics/graphics_object_base_property_group.cpp
  src/graphics/graphics_object_driver.cpp
  src/graphics/graphics_object_driver_table.cpp
  src/graphics/graphics_scene.cpp
  src/graphics/graphics_tree_node_mapping.cpp
  src/graphics/graphics_tree_node_mapping_driver.cpp
  src/graphics/graphics_tree_node_mapping_driver_table.cpp
  src/graphics/graphics_utils.cpp
  src/graphics/v3d_view_camera_animation.cpp
  src/graphics/v3d_view_controller.cpp

  src/gui/gui_application.cpp
  src/gui/gui_create_gfx_driver.cpp
  src/gui/gui_document.cpp
  src/gui/gui_document_list_model.cpp
  src/gui/qtgui_utils.cpp

  src/app/app_module.cpp
  src/app/button_flat.cpp
  src/app/dialog_about.cpp
  src/app/dialog_inspect_xde.cpp
  src/app/dialog_options.cpp
  src/app/dialog_save_image_view.cpp
  src/app/dialog_task_manager.cpp
  src/app/document_tree_node_properties_providers.cpp
  src/app/grid_helper.cpp
  src/app/item_view_buttons.cpp
  src/app/list_helper.cpp
  src/app/main.cpp
  src/app/mainwindow.cpp
  src/app/occt_window_740.cpp
  src/app/occt_window_750.cpp
  src/app/property_editor_factory.cpp
  src/app/property_item_delegate.cpp
  src/app/proxy_styled_item_delegate.cpp
  src/app/recent_files.cpp
  src/app/theme.cpp
  src/app/widget_clip_planes.cpp
  src/app/widget_file_system.cpp
  src/app/widget_gui_document.cpp
  src/app/widget_home_files.cpp
  src/app/widget_message_indicator.cpp
  src/app/widget_model_tree_builder.cpp
  src/app/widget_model_tree_builder_mesh.cpp
  src/app/widget_model_tree_builder_xde.cpp
  src/app/widget_model_tree.cpp
  src/app/widget_occ_view_controller.cpp
  src/app/widget_occ_view.cpp
  src/app/widget_properties_editor.cpp
  src/app/widget_shape_selector.cpp
  src/app/widgets_utils.cpp

  mayo.qrc

  src/app/dialog_about.ui
  src/app/dialog_inspect_xde.ui
  src/app/dialog_options.ui
  src/app/dialog_save_image_view.ui
  src/app/dialog_task_manager.ui
  src/app/mainwindow.ui
  src/app/widget_clip_planes.ui
  src/app/widget_model_tree.ui
  src/app/widget_properties_editor.ui

)
target_include_directories(
  ${PROJECT_NAME}
  PUBLIC
  ${CMAKE_CURRENT_BINARY_DIR} # version.h
  ${OpenCASCADE_INCLUDE_DIR}
  src/app
  src/3rdparty
)
target_link_libraries(
  ${PROJECT_NAME}
  Qt5::Widgets
  pthread
)

# FIXME CPack
