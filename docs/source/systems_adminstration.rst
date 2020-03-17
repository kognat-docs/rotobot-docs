*************************
System Adminstration Docs
*************************



Functional description 
=========================

Details of OpenFX Plugins
^^^^^^^^^^^^^^^^^^^^^^^^^

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
^^^^^^^^^^^^^^^^^^^^^^

Rotobot computations are lengthy in comparison to other compositing operations but are fast in comparison to doing rotoscoping by hand.

To this end rather than leaving Rotobot computations live to be recalculated in a script, it is worth writing the result to a non volatile location such as a hard disk drive as a file of the pixels what Rotobot has calculated.

The workflow should be the same as pre computing any part of a lengthy composite. See your technical lead to see if there is an automation of this process in your pipeline or in your OpenFX host software package.

Details of CUDA compatibility
=============================

CUDA Toolkit is installed with CuDNN dependency
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

CUDA is used to accelerate the computation of the deep neural networks that have been trained to deliver the Deep Learning solution of Rotobot.

CUDA is a technology made by NVIDIA and has several release versions.

Each CUDA version has a compatibility with the hardware driver of the NVIDIA GPU installed in your system.

Similarly the OpenFX host may make use of CUDA acceleration also.

There is a Deep Neural Network software library from NVIDIA called CuDNN. It has been at major version 7 for a number of years. Only the minor and patch version of this library have been updated.

CuDNN is always called the same thing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+
|Rotobot         | mac     | mac            | windows | windows        | windows        | windows        | linux       | linux       | linux          | linux         |
|Open FX Plugin  | 10.13+  | 10.13.6        | 10 x64  | 10 x64         | 10 x64         | 10 x64         | glibc 2.12+ | glibc 2.12+ | glibc 2.12+    | glibc 2.12+   |
|1.3.5           |         | cuda 10.0.130  |         | cuda 9.1.85    | cuda 9.2.148   | cuda 10.0.130  |             | cuda 9.1.85 | cuda 9.2.148   | cuda 10.0.130 |
|                | cpu     | cudnn 7.6.5.32 | cpu     | cudnn 7.6.3.30 | cudnn 7.5.0.56 | cudnn 7.6.5.32 | cpu         | cudnn 7.1.3 | cudnn 7.5.0.56 | cudnn 7.4.2   | 
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+
| NVIDIA Card    | 0       | 1              | 0       | 1              | 1 (RTX)        | 1 (RTX)        | 0           | 1           | 1 (RTX)        | 1  (RTX)      |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+
| Min Driver no  | na      | 410.10         | na      | 391.29         | 397.44         | 411.31         | na          | 390.46      | 397.44         | 411.31        |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+	
| Nuke 12 Linux  | na      | na             | na      | na             | na             | na             | Test Passed | Test Passed | Test Passed    | Test Passed   |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+
| Nuke 12 MacOS  | Passed  | Passed         | na      | na             | na             | na             | na          | na          | na             | na            |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+  
| Nuke 12 Windows| na      | na             | Passed  | Test Passed    | Test Passed    | Test Passed    | na          | na          | na             | na            |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+  
| Flame 2020.3   | na      | na             | na      | na             | na             | na             | Test Passed | Fail        | Fail           | Test Passed   |
| Linux          |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+  
| Flame 2020.3   | Passed  | Passed         | na      | na             | na             | na             | na          | na          | na             | na            |
| macOS          |         |                |         |                |                |                |             |             |                |               |	
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+  
| Fusion Studio  | na      | na             | na      | na             | na             | na             | Fail        | No test     | Fail           | No test       |
| 16.1 Linux     |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+  
| Fusion Studio  | Passed  | Passed         | na      | na             | na             | na             | na          | na          | na             | na            |
| 16.1 macOS     |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+  
| Fusion Studio  | na      | na             | Passed  | Fail           | Passed         | Fail           | na          | na          | na             | na            |
| 16.1 Windows   |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+  
|DaVinci Resolve |na       | na             | na      | na             | na             | na             | Passed      | Fail        | Pass           | Fail          |
| 16.1 Linux     |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+ 	
|DaVinci Resolve |na       | na             | Passed  | Fail           | Passed         | Fail           | na          | na          | na             | na            |
| 16.1 Windows   |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+ 
|DaVinci Resolve |Passed   | Passed         | na      | na             | na             | na             | na          | na          | na             | na            |
| 16.1 macOS     |1 CPU ?  |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+ 
| Natron 2.3.14  | na      | na             | na      | na             | na             | na             | Passed      | Passed      | Passed         | Passed        |
| Linux          |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+ 
| Natron 2.3.14  | na      | na             | Passed  | Passed         | Passed         | Passed         | na          | na          | na             | na            |
| Windows        |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+ 
| Natron 2.3.14  | Passed  | Passe          | na      | na             | na             | na             | na          | na          | na             | na            |
| macOS          |         |                |         |                |                |                |             |             |                |               |
+----------------+---------+----------------+---------+----------------+----------------+----------------+-------------+-------------+----------------+---------------+ 	


Details of memory requirements for models
=========================================

Rotobot ships with five deep learning models packaged in three plugins.

When using a CPU only version of the software 16Gb of available random access memory should be sufficient.

When using the NVIDIA GPU for computation, the amount of memory required and allocated on the first use of any of the nodes will vary and it will use the most memory available on the card to account for as many models that may be used during a Rotobot session.

From the the smallest model here are the memory requirements

Rotobot Instance Segmentation Standard: 2.8Gb
Rotobot Instance Segmentation Experimental: 3.8Gb
Rotobot Segmentation Standard: 4.2 Gb
Rotobot Segmentation Approximate: 3.2 Gb
Rotobot Trimap: 6.2 Gb

Memory allocation works as follows, once the first Rotobot node is computed, the Deep Neural network memory will be allocated and then recycled among the different models.

If you have 6.5 Gb of GPU memory free when the first node is computed you will have all nodes GPU accelerated. The amount of memory free will need to be 300Mb greater than the size of the model to allow for fluctuations in memory allocation.

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

OFX_PLUGIN_PATH
Rotobot will only be loaded if the rotobot.ofx.bundle is in the OFX_PLUGIN_PATH or the default OpenFX locations

ROTOBOT_MODEL_DIR
Will specify the default location of the files ending with .pb which are large trained neural network files.

PATH (Windows only)
This will need to include the shared_libraries subfolder from your install directory typically C:\Program Files\Kognat\shared_libraries


****************************
Systems Administration Guide
****************************


Installation
============

Network installation
^^^^^^^^^^^^^^^^^^^^

Installation on a single computer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^



Reporting a fault
^^^^^^^^^^^^^^^^^

	

	

	

