*************************
System Adminstration Docs
*************************



Functional description 
######################

Details of OpenFX Plugins
=========================

OpenFX plugins are shared libraries written in C/C++ which are initialised when an OpenFX host searches for executables.

The directories that are searched by default are

Windows:
::

    C:\Program Files\Common Files\OFX\Plugins

macOS:
::

    /Library/OFX/Plugins

Linux:
::

    /usr/OFX/Plugins

You can also search a number of paths using the environment variable
::

    OFX_PLUGIN_PATH

If the folder/bundle called rotobot.ofx.bundle appears in the default directories or the search path as specified by
::

    OFX_PLUGIN_PATH

in your runtime environment

Initially the plugin will attempt to load, some OpenFX hosts such as Foundry Nuke, will blacklist a plugin if it does not load on first attempt, which can be caused by missing dynamic libraries at the first attempt at running the plugin.

The simplest way to attempt to load a plugin for a second time is to find the file that ends in .ofx and update its date modified to the current time. Which can be done with command line tools.

Linux and macOS:
::

    touch rotobot.ofx 

Windows:
::

    copy /b rotobot.ofx +,,


Caching of computation
======================

Rotobot computations are lengthy in comparison to other compositing operations but are fast in comparison to doing rotoscoping by hand.

To this end rather than leaving Rotobot computations live to be recalculated in a script, it is worth writing the result to a non volatile location such as a hard disk drive as a file of the pixels what Rotobot has calculated.

The workflow should be the same as pre computing any part of a lengthy composite. See your technical lead to see if there is an automation of this process in your pipeline or in your OpenFX host software package.

Details of CUDA compatibility
=============================

CUDA Toolkit is installed with CuDNN dependency
-----------------------------------------------

CUDA is used to accelerate the computation of the deep neural networks that have been trained to deliver the Deep Learning solution of Rotobot.

CUDA is a technology made by NVIDIA and has several release versions.

Each CUDA version has a compatibility with the hardware driver of the NVIDIA GPU installed in your system.

Similarly the OpenFX host may make use of CUDA acceleration also.

There is a Deep Neural Network software library from NVIDIA called CuDNN. It has been at major version 7 for a number of years. Only the minor and patch version of this library have been updated.

CuDNN is always called the same thing
-------------------------------------

Windows:
::

    cudnn64_7.dll

macOS:
::

    libcudnn.7.dylib

Linux:
::

    libcudnn.so.7

The version of CuDNN is dependant on the version of CUDA Toolkit that the binary was used to link against the deep learning framework.

So while a OpenFX host may have chosen a version of CUDA Toolkit and CuDNN Rotobot need to match this version also, or it will see the file with an identical name and and try to use the binary routine and software symbols which are incompatible.

This will result in a crash, or even worse a hung computer.
For this reason, please choose the version of Rotobot that best matches your system with regard to hardware drivers and the compositing package you are using.

.. _rotobot-compatibility-table-label:

Rotobot Compatibility Table
===========================

+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+
|Rotobot         | mac     | mac            | windows | windows        | linux       | linux          | linux         |
|Open FX Plugin  | 10.13+  | 10.13.6        | 10 x64  | 10 x64         | glibc 2.12+ | glibc 2.12+    | glibc 2.12+   |
|1.3.5           |         | cuda 10.0.130  |         | cuda 9.2.148   |             | cuda 9.2.148   | cuda 10.0.130 |
|                | cpu     | cudnn 7.6.5.32 | cpu     | cudnn 7.5.0.56 | cpu         | cudnn 7.5.0.56 | cudnn 7.4.2   | 
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+
| NVIDIA Card    | 0       | 1              | 0       | 1 (RTX)        | 0           | 1 (RTX)        | 1  (RTX)      |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+
| Min Driver no  | na      | 410.10         | na      | 397.44         | na          | 397.44         | 411.31        |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+	
| Nuke 12 Linux  | na      | na             | na      | na             | Test Passed | Test Passed    | Test Passed   |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+
| Nuke 12 MacOS  | Passed  | Passed         | na      | na             | na          | na             | na            |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+  
| Nuke 12 Windows| na      | na             | Passed  | Test Passed    | na          | na             | na            |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+  
| Flame 2020.3   | na      | na             | na      | na             | Test Passed | Fail           | Test Passed   |
| Linux          |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+  
| Flame 2020.3   | Passed  | Passed         | na      | na             | na          | na             | na            |
| macOS          |         |                |         |                |             |                |               |	
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+  
| Fusion Studio  | na      | na             | na      | na             | Fail        | Fail           | No test       |
| 16.1 Linux     |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+  
| Fusion Studio  | Passed  | Passed         | na      | na             | na          | na             | na            |
| 16.1 macOS     |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+  
| Fusion Studio  | na      | na             | Passed  | Passed         | na          | na             | na            |
| 16.1 Windows   |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+  
|DaVinci Resolve |na       | na             | na      | na             | Passed      | Pass           | Fail          |
| 16.1 Linux     |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+ 	
|DaVinci Resolve |na       | na             | Passed  | Passed         | na          | na             | na            |
| 16.1 Windows   |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+ 
|DaVinci Resolve |Passed   | Passed         | na      | na             | na          | na             | na            |
| 16.1 macOS     |1 CPU ?  |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+ 
| Natron 2.3.14  | na      | na             | na      | na             | Passed      | Passed         | Passed        |
| Linux          |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+ 
| Natron 2.3.14  | na      | na             | Passed  | Passed         | na          | na             | na            |
| Windows        |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+ 
| Natron 2.3.14  | Passed  | Passed         | na      | na             | na          | na             | na            |
| macOS          |         |                |         |                |             |                |               |
+----------------+---------+----------------+---------+----------------+-------------+----------------+---------------+ 	


Details of memory requirements for models
=========================================

Rotobot ships with five deep learning models packaged in three plugins.

When using a CPU only version of the software 16Gb of available random access memory should be sufficient.

When using the NVIDIA GPU for computation, the amount of memory required and allocated on the first use of any of the nodes will vary and it will use the most memory available on the card to account for as many models that may be used during a Rotobot session.

From the the smallest model here are the memory requirements

+----------------------------------------+----------------------------------+
| Rotobot Model                          | Required Free CUDA Memory on GPU |
+----------------------------------------+----------------------------------+
| Instance Segmentation Standard         | 4.0 Gb                           | 
+----------------------------------------+----------------------------------+
| Segmentation Approximate               | 4.4 Gb                           |
+----------------------------------------+----------------------------------+
| Instance Segmentation Experimental     | 5.0 Gb                           |
+----------------------------------------+----------------------------------+
| Segmentation Standard                  | 5.4 Gb                           |
+----------------------------------------+----------------------------------+
| Trimap                                 | 8.1 Gb                           |
+----------------------------------------+----------------------------------+

Memory allocation works as follows, once the first Rotobot node is computed, the Deep Neural network memory will be allocated and then recycled among the different models.

If you have 6.5 Gb of GPU memory free when the first node is computed you will have all nodes GPU accelerated. The amount of memory free will need to be 300Mb greater than the size of the model to allow for fluctuations in memory allocation.

This suggest for best performance a 8 Gb card with about 7 Gb of free memory will give best results with Rotobot.

Multi GPU Performance
=====================

Memory will be used on each available GPUs one at a time for each instance of Rotobot.

Once a each GPU has a single Rotobot session running on each GPU a second will fit as many of the above models as memory is available.

Application Note: On a AWS box with 4 Telsa T4 Turing cards each with 15109MiB of RAM, eight Rotobot models running the greatest model were able to be run concurrently without issue under Amazon Linux with Natron 2.3.4 as an OpenFX Host. 

Limitations of Resolution
=========================

Instance Segmentation has very limited resolution but can look great when what it is detected is small in screen size.

If the object is beyond 100 x 100 pixels in screen size, you will start to get blocky artifacts, this is by design as Instance Segmentation can detect a number of objects, and you can choose each object, whose bounding box intersects with a pixel coordinate. Ticking the experimental box will double the effective resolution, but beyond 150x150 pixels things will continue to look blocky.

Segmentation is currently limited to 2049 x 2049 in screen resolution, as a result 1080p in portrait or landscape is roughly the upper limit which will give reasonable detection, but edges will only be detected to within a margin of +/- four pixels of an edge.

By this logic, if you detect at 1080p and scale down to 360p you can get a near perfect edge.

Similarly Rotobot Trimap has a resolution limit of 2048x2048, which will cover up to 1080p footage. The quality of the result will vary, but if the edge lies in the “grey” region of the trimap hint mask it will give a good estimate provided there is enough correlation between your image and what Rotobot was trained on.

Colour Space information
========================

Colour science is a large topic. 

There are some excellent general notes on the topic here:

VES Cinematic Color: http://github.com/jeremyselan/cinematiccolor/raw/master/ves/Cinematic_Color_VES.pdf

It makes sense for pixel filters and similar used in Digital Content Creation packages such as a compositing package to work in Scene Linear colour space, such as ACEScg, where the relationship of the pixel value and the amount of light in a real world scene have a linear relationship.

Display Space for an sRGB monitor is what Rotobot was trained on. This means that while a Scene Linear value for mid grey is approximately 0.2, a Display Space sRGB mid grey will have a value of approximately 0.5, half way between zero and one. In a scene linear scale to get a grey that is exposure value lighter, which you can get by doubling the shutter exposure time, you would expect to double the value from roughly 0.2 to roughly 0.4. But in a Display Space sRGB to make the same brightness increase you only need a value from 0.5 to 0.7, which is much less than doubling.

If you cannot tell which colour space your data is in, if you can find a way to multiply the data by two a number of times, if it feel like it is getting brighter very quickly, chances you are in Display Space, if you double your data and it gets brighter gradually, chances are you are Scene Linear space, which is linear in its relationship to light.

The simplest way to convert from one set of values to another is to use a Colour Transform node in your composting package and move from the colour space you are working in to the sRGB Display space.

OCIO Color Transform from the OpenColor IO project has from and to spaces and it is a matter of knowing your input source colour space and your output target should be a display sRGB, where a mid grey is around 0.5. These are available in Nuke, Natron, Fusion and the Fusion Panel of Resolve and will depend on your OCIO configuration. Flame has very complete colour management.

As a rule of thumb, if your image looks pale with the lookup table and looks natural without the lookup table, this is the expected input for a Display sRGB image.

Details of Environment variables
================================
::

    OFX_PLUGIN_PATH

Rotobot will only be loaded if the rotobot.ofx.bundle is in the OFX_PLUGIN_PATH or the default OpenFX locations

::

    ROTOBOT_MODEL_DIR

Will specify the default location of the files ending with .pb which are large trained neural network files.

::

    PATH

(Windows only)
This will need to include the shared_libraries subfolder from your install directory typically

::

    C:\Program Files\Kognat\shared_libraries


Systems Administration Guide
############################

Installing Rotobot should be trivial!

But to make sure it is here are some guides, where possible we have forced Rotobot installers to use the Administration account and install to standard places.

We are aware that many larger companies, who use Linux, use networked stores for the software locations which vary from studio to studio.

For this reason we do NOT force Administration or super user rights for Linux installation.

As a result if you use a standard user account rather than the administration user account some of the default functionality of the install wont work.

But you can follow the network install guide to get things working, if you do not have super user rights.

Installation
============

Download the installer with the following executable formats after the installer archive has been extracted

Windows

::

   <installer_name>.exe

Linux

::

    <installer_name>.run

MacOS

::

   <installer_name>(.app)


On Windows and macOS, you need to double click on the installers graphically for default behaviour, which will escalate permissions to the Administration user and install to the default location

Default Install Locations
-------------------------

Windows

::

   C:\Program Files\Kognat

MacOS

::

   /Applications/Kognat

Linux

::

    /opt/Kognat



Components Installed
====================

Deep Learning Models
--------------------

There should be five deep learning models with the ``.pb`` file extension

Open FX Folder/Bundle
---------------------

There should be a folder/bundle called ``rotobot.ofx.bundle`` this contains the executable binary and in the case of macOS and Linux all the support shared libraries

Shared Libraries
----------------

On macOS and Linux, the shared libraries ending in ``.so`` for Linux and ``.dylib`` for macOS are in the relative rpath to the ``rotobot.ofx`` binary

On Windows the supporting shared libraries or ``.dll`` binaries are in a sub folder called ``shared_libraries`` this needs to be on the ``%PATH%`` system environment variable

The installer will add this folder to the path

Main OpenFX Plugin
------------------

There is a file called ``rotobot.ofx`` which is the heart of the software, which is the pulled on by the OpenFX host program, your compositing package.


License Files
-------------

There is a subfolder with the following components used by Reprise License Manager the license management system see :ref:`licensing`. 



RLM License Utility
^^^^^^^^^^^^^^^^^^^

macOS and Linux

::

    rlmutil

Windows

::


    rlmutil.exe

This executable can be used to identify your rlmhost id for signing a license by Kongat staff

RLM Server
^^^^^^^^^^

macOS and Linux

::

    rlm

Windows

::

    rlm.exe

These files are used to host the RLM Server


RLM Independent Software Vendor Settings file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All Operating Sytems

::

    kognat.set

This file allows the decryption of the license system with the settings for the Kognat as a independant software vendor using the RLM system.


Installation on a single computer
=================================

This is the default use of the installer using Administrator permissions.

Windows
-------

1. Extract the zip folder
2. Within the ``installer`` folder double click the Install Builder executable ``<name>.exe``
3. If you see security warnings, the software signature process is incomplete, use your judgement to ignore warnings
4. Allow Administration rights for the installer
5. Follow the default choices.
6. Software install should be complete, after the window closes, it should take less than two minutes on a reasonably fast disk.


MacOS
-----

1. Extract the zip folder
2. Within the ``installer`` folder double click the Install Builder executable
3. If you see security warnings, the software signature process is incomplete, use your judgement to ignore warnings
4. Allow Administration rights for the installer
5. Follow the default choices.
6. Software install should be complete, after the window closes, it should take less than two minutes on a reasonably fast disk.

Linux
-----

1. Extract the zip folder
2. Within the ``installer`` folder double click the Install Builder executable ending in the file extension ``.sh``
3. Allow Administration rights for the installer by using the GUI or follow the guide below.
4. In a GUI open a Command Prompt at the folder with the ``<installername>.sh`` file inside
5. Within this folder in the commnd prompt CLI execute ``sudo ./*.sh`` and give the password
6. Follow the default choices on the GUI.
7. Software install should be complete, after the window closes, it should take less than two minutes on a reasonably fast disk.

Network installation
====================

Linux
-----

Looking at the Bit Rock Install Builder command line help we can see the following

::

    Kognat Rotobot OpenFX Plugin X.Y.Z-cpu-only
    Usage:
    
     --help                                      Display the list of valid options

     --version                                   Display product information
     
     --unattendedmodeui <unattendedmodeui>       Unattended Mode UI
                                                 Default: none
                                                 Allowed: none minimal minimalWithDialogs
    
     --optionfile <optionfile>                   Installation option file
                                                 Default: 
    
     --debuglevel <debuglevel>                   Debug information level of verbosity
                                                 Default: 2
                                                 Allowed: 0 1 2 3 4
    
     --mode <mode>                               Installation mode
                                                 Default: gtk
                                                 Allowed: gtk xwindow text unattended
    
     --debugtrace <debugtrace>                   Debug filename
                                                 Default: 
    
     --installer-language <installer-language>   Language selection
                                                 Default: en
                                                 Allowed: sq ar es_AR az eu pt_BR bg ca hr cs da nl en et fi fr de el he hu id it ja kk ko lv lt no fa pl pt ro ru sr zh_CN sk sl es sv th zh_TW tr tk va vi cy
    
     --prefix <prefix>                           Installation Directory
                                                 Default: /home/sam/Kognat


1. Create a folder where you would like to unpack the contents of the installer
2. in a ``bash`` shell create an environment variable to refer to this folder

::

     export DESTINATION=<fullpath_to_folder_in_step_1>

3. change directories into the ``installer`` folder where you unzipped the ``.sh`` large installer file.
4. Put the following into a shell

::

    ./*.sh --mode unattended --prefix $DESTINATION

5. Then change to the 

::

   cd $DESTINATION

6. Now you have `Components Installed`_ rather than being in `Default Install Locations`_  they are now in the folder you created which is your current directory.
7. To use the software from this folder, it is simply a matter of setting some runtime environment variables see `Details of Environment variables`_.
8. Append to ``OFX_PLUGIN_PATH`` to include the folder containing ``rotobot.ofx.bundle``
9. Create and set an environment variable in your runtime environment for ``ROTOBOT_MODEL_DIR`` to a fast disk which has a folder containing the files with the ``.pb`` extension
10. Maybe for a quick test the following will work for a ``bash`` shell

::

   export OFX_PLUGIN_PATH="${OFX_PLUGIN_PATH}:${PWD}"
   export ROTOBOT_MODEL_DIR="${PWD}"

11. You can now put this in a more permanent location or write tools to automate this process for network installations
12. A good standard runtime environment can be found here: https://github.com/nerdvegas/rez/blob/master/README.md

Rez example file
----------------

::

    user@mtl-rmw001l rotobot $ cat package.py 
    # pylint: disable=invalid-name
    name = 'rotobot'

    version = '1.3.5'

    authors = ['Kognat']

    description = 'AI driven rough rotoscoping OFX plugin.'

    requires = ['nuke-10+']

    # Requirements used during the build process only.
    # Here "rdo_package_utils" is our library used to build packages.
    private_build_requires = ['rdo_package_utils']

    uuid = ''

    # This tells to rez how to build the package.
    build_command = 'python {root}/build.py'

    def commands():
        """Commands that will be ran at the execution of rez-env."""
        import os
        env = locals()['env']  # silence linters
        pluginLocation = os.path.join('{root}', 'resources', 'linux', 'nuke')
        env.OFX_PLUGIN_PATH.append(pluginLocation)
        env.ROTOBOT_MODEL_DIR.append(pluginLocation)
        env.kognat_LICENSE.append('8053@licsrv01')

Reporting a fault
=================


Requesting a feature
====================	

	

	

