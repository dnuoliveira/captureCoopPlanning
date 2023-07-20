# captureCoopPlanning
Cooperative Planning for CAPTURE project. Currently in development.

This package assumes the correct installation and setup of the repository https://github.com/hardtekpt/M690B-Wiki, and the the smach-viewer package (sudo apt-get install smach-viewer). To use this package just add it to the catkin workspace.

To run the simulation follow the next steps:

* run the simulator_bringup_cooperative_planing.launch file. This file starts the simulation of both drones and starts the shuttle's controller.
* the target's control is currently done by QGroundControl. In this package there's a mission file (fixed_wing_dubins_path_mission), when the simulation is running, upload the file to the target drone in QGroundControl (vehicle 2) and start the mission so the drone follows the trajectory.
* After the shuttle's takeoff, in another terminal window, start the state machine node with the command "rosrun cooperative_planning state_machine.py", and start the state machine viewer with the command "rosrun smach_viewer smach_viewer.py". The controller will start to receive the state machine's instructions.
* When the shuttle is in the state "IDLE_NOT_READY", it will wait for the user's input to start the maneuvers. To do this, use the command "rostopic pub -1 /cooperative_planning/state_machine/start_command std_msgs/Empty" to send the start command to the state machine and trasition to the state where it will wait for the target drone to start moving.

The shuttle drone should perform a really rough "capture maneuver" while trying to position himself on top of the target drone, following the states described in the state machine.


