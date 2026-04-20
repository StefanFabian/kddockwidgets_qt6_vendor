cmake_minimum_required(VERSION 3.15)
project(kddockwidgets_qt6_vendor)

find_package(ament_cmake REQUIRED)
find_package(ament_cmake_vendor_package REQUIRED)

ament_vendor(kddockwidgets_qt6_vendor
  VCS_URL https://github.com/KDAB/KDDockWidgets.git
  VCS_VERSION v2.4.0
  GLOBAL_HOOK
  CMAKE_ARGS
    "-C${CMAKE_CURRENT_SOURCE_DIR}/cmake/kddockwidgets_qt6_vendor-build-options.cmake"
)

configure_file(
  cmake/kddockwidgets_qt6_vendor-extras.cmake.in
  "${CMAKE_CURRENT_BINARY_DIR}/kddockwidgets_qt6_vendor-extras.cmake"
  @ONLY
)

if(BUILD_TESTING)
  include(CTest)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
  find_package(Qt6 REQUIRED COMPONENTS Widgets Quick QuickControls2)

  set(KDDOCKWIDGETS_QT6_VENDOR_SMOKE_TEST_DIR
    "${CMAKE_CURRENT_BINARY_DIR}/kddockwidgets_qt6_vendor_smoke_test")
  configure_file(
    cmake/CMakeLists.smoke_test.in
    "${KDDOCKWIDGETS_QT6_VENDOR_SMOKE_TEST_DIR}/CMakeLists.txt"
    @ONLY
  )

  add_test(
    NAME kddockwidgets_qt6_vendor_smoke_test
    COMMAND ${CMAKE_COMMAND}
      -S "${KDDOCKWIDGETS_QT6_VENDOR_SMOKE_TEST_DIR}"
      -B "${KDDOCKWIDGETS_QT6_VENDOR_SMOKE_TEST_DIR}/build"
  )
endif()

ament_package(
  CONFIG_EXTRAS "${CMAKE_CURRENT_BINARY_DIR}/kddockwidgets_qt6_vendor-extras.cmake"
)
