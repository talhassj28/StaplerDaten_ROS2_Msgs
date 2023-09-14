cmake_minimum_required(VERSION 3.5)
project(sbg_driver)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(std_msgs REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

set(msg_files
  "msg/SbgAirData.msg"
  "msg/SbgAirDataStatus.msg"
  "msg/SbgEkfEuler.msg"
  "msg/SbgEkfNav.msg"
  "msg/SbgEkfQuat.msg"
  "msg/SbgEkfStatus.msg"
  "msg/SbgEvent.msg"
  "msg/SbgGpsHdt.msg"
  "msg/SbgGpsPos.msg"
  "msg/SbgGpsPosStatus.msg"
  "msg/SbgGpsRaw.msg"
  "msg/SbgGpsVel.msg"
  "msg/SbgGpsVelStatus.msg"
  "msg/SbgImuData.msg"
  "msg/SbgImuShort.msg"
  "msg/SbgImuStatus.msg"
  "msg/SbgMagCalib.msg"
  "msg/SbgMag.msg"
  "msg/SbgMagStatus.msg"
  "msg/SbgOdoVel.msg"
  "msg/SbgShipMotion.msg"
  "msg/SbgShipMotionStatus.msg"
  "msg/SbgStatusAiding.msg"
  "msg/SbgStatusCom.msg"
  "msg/SbgStatusGeneral.msg"
  "msg/SbgStatus.msg"
  "msg/SbgUtcTime.msg"
  "msg/SbgUtcTimeStatus.msg"
)

rosidl_generate_interfaces(${PROJECT_NAME}
  ${msg_files}
)

ament_export_dependencies(rosidl_default_runtime)

install(
  FILES sbg_mapping_rules.yaml
  DESTINATION share/${PROJECT_NAME})

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
