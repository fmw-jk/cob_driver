project(cob_trajectory_controller)

catkin_project(${PROJECT_NAME}
	INCLUDE_DIRS common/include
	DEPENDS Boost Orocos-KDL
)

include_directories(common/include)

# service generation
find_package(genmsg REQUIRED)
find_package(ROS REQUIRED std_msgs)
include_directories(${ROS_INCLUDE_DIRS})

add_service_files(DIRECTORY srv FILES SetFloat.srv)

generate_messages(DEPENDENCIES std_msgs)


# executables
find_package(Boost REQUIRED thread)
include_directories(${Boost_INCLUDE_DIRS}) #SYSTEM ?

find_package(orocos_kinematics_dynamics REQUIRED)
include_directories(${orocos_kinematics_dynamics_INCLUDE_DIRS})
link_directories(${orocos_kinematics_dynamics_LIBRARY_DIRS})

add_executable(${PROJECT_NAME} ros/src/${PROJECT_NAME}.cpp common/src/genericArmCtrl.cpp common/src/RefValJS_PTP.cpp common/src/RefValJS_PTP_Trajectory.cpp common/src/TimeStamp.cpp)
add_executable(cob_simulation_tester ros/src/cob_simulation_tester.cpp)

target_link_libraries(${PROJECT_NAME} ${Boost_LIBRARIES})


# install all manifests; for compatibility with old build system
install(FILES manifest-to-install.xml 
	DESTINATION share/cob_srvs RENAME manifest.xml)
