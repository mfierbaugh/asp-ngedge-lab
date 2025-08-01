# Features 

This project has been modified from it's original form and is meant to be run in dcloud on ContainerLabs hosts. 
Authors: Marty Fierbaugh (mfierbau@cisco.com), Chris Olson (christoo@cisco.com)

Features in this playbook:
 - Segment Routing v6 uSID using ISIS
 - Transport Independant Loop Free Alternate (TI-LFA)
 - Flexable Algorithm
 - Model-Driven Telemetry
 - Segment Routing Performance Measurement (SR-PM)
 - BGP with PIC Edge/Core

## Devices
- Cisco 8712-MOD running IOS-XR 25.2.1 (PE) 
- Cisco XRd running IOS-XR 25.2.1 (CE and CORE)
- Cisco T-Rex ver 3.06 (Trex-1, Trex-2)

# Usage

1. Start the lab using clab deploy (or by using the same method within the VSCode plugin)
2. Once nodes are fully up, use ./config lab to build and push configurations to the nodes. 

NOTE: 8712-MOD can take ~20 mins to fully boot.  Use docker logs -f to monitor progress.  "Router up" indicates the node is fully booted.

# Setup

Start by updating the host field to mach your enviroment.
.
..
...

# Run playbooks directly

To run the playbook without committing changes:

    ansible-playbook -i hosts.yml lab_master_playbook.yml -e "commit_changes=0"

To run the playbook committing the changes:

    ansible-playbook -i hosts.yml clab_master_playbook.yml -e "commit_changes=1"

The following script just simply execute the second example and commits changes

./config_lab




# Start T-REX 

# Start the interactive trex console which will make a local connection to the running interactive daemon
./trex-console

# Start generating some traffic
start -f stl/imix.py

# To interact with and view statistics for the current stream launch the text-based user interface (tui)
tui

# Attempt to increase per interface traffic rate to 200mbps (400mbps rx/tx total). Throughput achievable in the Docker environment is dependent primarily on single core\thread CPU performance.
update -m 200mbps
