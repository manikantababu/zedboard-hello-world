Zedboard hello world
====================

Issue: I cloned this repo and then "made all" but it looks like the "Write Project TCL.." didn't save the
software, so I have to look at seeing how to preserve the software.

Here is a way to use git with Vivado. The project is a
Zedboard Hello World project with no content in the
PL (Programmable logic) and only a trivial Hello World
for the ARM as generated by the Xilinx SDK.

* Create  a vivado project and get it “working”
* Use File > Write Project Tcl.. navigate to the local project directory and write Build.tcl file.
* Add the following Makefile to the project changing GENERATED_DIR:

```
wink@ssi-primary:~/prgs/vivado-base-project-x$ cat Makefile
# GENERATED_DIR is the generated vivado project directory
# it will need to be changed to your project

GENERATED_DIR = vivado-base-project
VIVADO_DIR = /opt/Xilinx/Vivado/2014.4
VIVADO_EXE = $(VIVADO_DIR)/bin/vivado

all:
	   $(VIVADO_EXE) -mode batch -source build.tcl -notrace

clean:
	   @ rm -rf $(GENERATED_DIR) vivado.log vivado.jou
```

* Edit Makefile changing GENERATED_DIR to the name of the project file.
* Run make clean which will remove all unnecessary files.
* Create a git repo in the directory saving all of the files.
* Run make all which will re-create the vivado project.

```
wink@ssi-primary:~/prgs/vivado-base-project-x$ make all
/opt/Xilinx/Vivado/2014.4/bin/vivado -mode batch -source build.tcl -notrace

****** Vivado v2014.4 (64-bit)
  **** SW Build 1071353 on Tue Nov 18 16:47:07 MST 2014
  **** IP Build 1070531 on Tue Nov 18 01:10:18 MST 2014
    ** Copyright 1986-2014 Xilinx, Inc. All Rights Reserved.

source build.tcl -notrace
WARNING: [Board 49-26] cannot add Board Part xilinx.com:kc705:part0:0.9 available at /opt/Xilinx/Vivado/2014.4/data/boards/board_parts/kintex7/kc705/0.9/board_part.xml as part xc7k325tffg900-2 specified in board_part file is either invalid or not available
WARNING: [Board 49-26] cannot add Board Part xilinx.com:kc705:part0:1.0 available at /opt/Xilinx/Vivado/2014.4/data/boards/board_parts/kintex7/kc705/1.0/board_part.xml as part xc7k325tffg900-2 specified in board_part file is either invalid or not available
WARNING: [Board 49-26] cannot add Board Part xilinx.com:kc705:part0:1.1 available at /opt/Xilinx/Vivado/2014.4/data/boards/board_parts/kintex7/kc705/1.1/board_part.xml as part xc7k325tffg900-2 specified in board_part file is either invalid or not available
WARNING: [Board 49-26] cannot add Board Part xilinx.com:zc706:part0:0.9 available at /opt/Xilinx/Vivado/2014.4/data/boards/board_parts/zynq/zc706/0.9/board_part.xml as part xc7z045ffg900-2 specified in board_part file is either invalid or not available
WARNING: [Board 49-26] cannot add Board Part xilinx.com:zc706:part0:1.0 available at /opt/Xilinx/Vivado/2014.4/data/boards/board_parts/zynq/zc706/1.0/board_part.xml as part xc7z045ffg900-2 specified in board_part file is either invalid or not available
WARNING: [Board 49-26] cannot add Board Part xilinx.com:zc706:part0:1.1 available at /opt/Xilinx/Vivado/2014.4/data/boards/board_parts/zynq/zc706/1.1/board_part.xml as part xc7z045ffg900-2 specified in board_part file is either invalid or not available
WARNING: [Project 1-153] The current project part 'xc7k70tfbg676-1' does not match with the 'EM.AVNET.COM:ZED:PART0:1.2' board part settings. The project part will be reset to 'EM.AVNET.COM:ZED:PART0:1.2' board part.
INFO: [Project 1-152] Project part set to zynq (xc7z020clg484-1)
INFO: Project created:vivado-base-project
INFO: [Common 17-206] Exiting Vivado at Fri Dec 26 07:50:16 2014...
```
