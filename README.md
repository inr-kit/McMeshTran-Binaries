**************************************************************************************
McMeshTran: A MC Mesh and data Transformation/ Translation/ Transfer tool

McMeshTran provide post-processing interface for MCNP mesh tally, MCNP6 unstructured mesh output and TRIPOLI mesh tally, and multiphics coupling with Fluent, CFX, and ANSYS Workbench. It provide useful functions such as summing, averaging mesh tally, tranforming mesh and interpolate data. 

For any questions related to the use of this software/library you may contact Ulrich Fischer(ulrich.fischer@kit.edu) or, for technical assistance, Yuefeng Qiu (yuefeng.qiu@kit.edu).
**************************************************************************************
********Something to know before going on********

This document describes the procedure of installing  binaries. For compiling McMeshTran, please find descriptions on Github repository "McMeshTran-Source". For Using McMeshTran, Please find documents on Github repository "McMeshTran-Docs".

This release is tested under Salome_7.4.0. Using other Salome version is not guarantee to work, and might cause error during this process. 


**************************************************************************************
********Installation and run McMeshTran on Windows ********

* Download Salome_7.4.0 platform from http://www.salome-platform.org/downloads/previous-versions/salome-v7.4.0 . 

  * The version you need is "binaries self-extracting archive for 64bits Windows". 
	
  * You need to register for downloading Salome. 

* Extract the Package into a folder, here brief as $SALOME (be sure to replace it with actual path during installation). 

* Download the "MCMESHTRAN_0.1.0-beta_for_Salome_7.4.0_WIN64.zip", extract it and place it under $SALOME/MODULES. Under $SALOME\MODULES\MCMESHTRAN there are three folder: 

  * bin
  * lib
  * share
	
* We need to add MCMESHTRAN into the Salome environment. First make a backup of file $SALOME\env_launch.bat

  * in line 29, add "MCMESHTRAN" into the "m_list" (add it anywhere inside the parenthesis, separate with at least one whitespace)
	
  * in line 42, add "GUI GEOM MED SMESH PARAVIS MCMESHTRAN" into "env_m_list"(add them inside the parenthesis, separate with at least one whitespace).

* To run McMeshTran, start cmd.exe in the Windows Start menu, and run the following command:

  * $SALOME\run_salome.bat --module=MCMESHTRAN
	
  * If you want to start also geometry, meshing and visualization module, using command: $SALOME\run_salome.bat --module=GEOM,SMESH,PARAVIS,MCMESHTRAN
	
* One more easy way to run the program is:

  * right-click $SALOME\run_salome.bat and "Send to -> Desktop (short-cut)";
	
  * right-click the short-cut link in the Desktop, choose "properties";
	
  * Behind the value of "Target", add " --module=MCMESHTRAN" or "
	--module=GEOM,SMESH,PARAVIS,MCMESHTRAN"(with a whitespace in the front). click "OK". Next time you can start McMeshTran with this short-cut link. 

* Notes: it is found that McMeshTran Windows version is failed in sending data to ParaView. We will fix this later. 

**************************************************************************************
********Installation and run McMeshTran on Linux ********

* Download Salome_7.4.0 platform from http://www.salome-platform.org/downloads/previous-versions/salome-v7.4.0 . 

  * Under the list "Binaries for officially supported Linux platforms", Choose the version which is closest to your OS. 
	
  * You need to register for downloading Salome. 


* Extract the zip file into a folder, then go into this folder and run the script "runInstall". A install wizard window will come out. 

* Click always "Next", and keep the default value if you don't care.

  * If you like, you can change the installation folder;
	
  * If you want to save disk space, choose only these module : KERNEL, GUI, MED, GEOM, SMESH, PARAVIS.
	
  * There might be warnings on "cppunit" libraries and so on, it won't affect the use of Salome. 
	
* We abbreviate the Salome install folder as $SALOME.

* Download the corresponding McMeshTran binary. Try to choose the version closest to your OS. If it does not work after the following installation, the only solution is to download the McMeshTran source code and compiled the binary by yourself. 

* Extract the zip file and place it under $SALOME. Be sure that your $SALOME/MCMESHTRAN_0.1.0 folder have following folders:

  * bin
  * lib
  * share
  * adm_local
  * idl
  * include

* Open $SALOME/KERNEL_7.4.0/salome.sh, add the following environment variables into this file.
```
	#------ MCMESHTRAN ------
	export MCMESHTRAN_ROOT_DIR=${INST_ROOT}/MCMESHTRAN_0.1.0
	if [ -n "${ENV_FOR_LAUNCH}" ] ; then
	  if [ "${ENV_FOR_LAUNCH}" = "1" ] ; then
		exportp PATH ${MCMESHTRAN_ROOT_DIR}/bin/salome
		exportp LD_LIBRARY_PATH ${MCMESHTRAN_ROOT_DIR}/lib/salome
		exportp PYTHONPATH ${MCMESHTRAN_ROOT_DIR}/bin/salome:${MCMESHTRAN_ROOT_DIR}/lib/python${PYTHON_VERSION}/site-packages/salome
	  fi
	fi
	##
	#------ MCMESHTRAN_src ------
	export MCMESHTRAN_SRC_DIR=${INST_ROOT}/MCMESHTRAN_SRC_0.1.0
```
-> In your desktop, create a new file "runSalome.sh" and put following text into this file(replacing $SALOME with actual path!!): 
```
	#!/bin/bash
	source $SALOME/KERNEL_7.4.0/salome.sh
	$SALOME/salome_appli_7.4.0/salome --module=GEOM,SMESH,PARAVIS,MCMESHTRAN
```
* Under Desktop, make this file as executable script using this command:

	chmod +x ./runSalome.sh

* You can run McMeshTran with running this script now. 


**************************************************************************************
For more information, you can find in our publications.

* Yuefeng Qiu, Lei Lu, Ulrich Fischer, Integrated approach for fusion multi-physics coupled analyses based on hybrid CAD and mesh geometries, Fusion Engineering and Design, Available online 4 July 2015, ISSN 0920-3796, http://dx.doi.org/10.1016/j.fusengdes.2015.06.118.

* Yuefeng Qiu, Peng Lu, Ulrich Fischer, Pavel Pereslavtsev, Szabolcs Kecskes, A generic data translation scheme for the coupling of high-fidelity fusion neutronics and CFD calculations, Fusion Engineering and Design, Volume 89, Issues 7–8, October 2014, Pages 1330-1335, ISSN 0920-3796, http://dx.doi.org/10.1016/j.fusengdes.2014.02.044.

Have fun!
