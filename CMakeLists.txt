cmake_minimum_required(VERSION 2.8)
project(cob_driver)

find_package(catkin REQUIRED)

catkin_stack()

foreach(SUBDIR
    cob_base_drive_chain
    cob_base_velocity_smoother
    cob_camera_sensors
    cob_canopen_motor
    cob_collision_velocity_filter
    cob_footprint_observer
    cob_generic_can
    cob_head_axis
    cob_hokuyo
    cob_light
    cob_phidgets
    cob_relayboard
    cob_sick_s300
    cob_sound
    cob_touch
    cob_trajectory_controller
    cob_undercarriage_ctrl
    cob_utilities
    )
  add_subdirectory(${SUBDIR})
endforeach()

