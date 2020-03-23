Choosing an Installer for Rotobot
=================================

Rotobot exists for three 64 bit operating systems:
 * macOS 64 bit (10.13+ and 10.13 for CUDA support)
 * Linux 64 bit (glibc 2.12 and above)
 * Windows 64 bit (10)

You can narrow your search by looking at the installers for your operating system only.

If you have no NVIDIA hardware, then you have one choice which is the CPU only version for your operating system.

If you do have NVIDIA hardware, you initially are limited by your driver version you have installed, we do not recommend updating hardware drivers, from what is recommended by your hardware vendor and software vendor of your digital content creation package.


+----------------+---------------------+-------------------------+---------------------+
| CUDA VERSION   | Linux Kernel Driver | Windows Hardware Driver | macOS CUDA Driver   |
+----------------+---------------------+-------------------------+---------------------+
| CUDA 10.0      | >= 410.48           | >= 411.31               | 410.130             |
| (10.0.130)     |                     |                         | (macOS: 10.13.x)    |
+----------------+---------------------+-------------------------+---------------------+
| CUDA 9.2       | >= 396.37           | >= 398.26               |                     |
| (9.2.148 upd 1)|                     |                         |                     |
+----------------+---------------------+-------------------------+---------------------+
| CUDA 9.1       | >= 390.46           | >= 391.29               |                     |
| (9.1.85)       |                     |                         |                     |
+----------------+---------------------+-------------------------+---------------------+
| CUDA 9.0       | >= 384.81           | >= 385.54               |                     |
| (9.0.76)       |                     |                         |                     |
+----------------+---------------------+-------------------------+---------------------+



Install packages Guidance
^^^^^^^^^^^^^^^^^^^^^^^^^

 * Blackmagic Design's products (Standalone Fusion Studio 
   and DaVinci Resolve with the Fusion Panel) that are 
   current version (16.0)
   need CUDA 9.2 for all operating systems.

 * Autodesk's Flame needs CUDA 10.0 if using NVIDIA.

 * Foundry's Nuke can work with
   CUDA 9.0, CUDA 9.1 CUDA 9.2 and CUDA 10.0

 * Turing Chipset cards RTX based series
   need CUDA 9.2 or CUDA 10.0 to support acceleration.

 * CPU versions work with all 
   applications and they are 
   perfect for a CPU only renderfarm

See :ref:`rotobot-compatibility-table-label` documents for more details:

