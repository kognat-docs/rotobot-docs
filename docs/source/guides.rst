
***********
User Guides
***********

Rotobot should be fairly self explanatory to use.

There are a number of checkboxes with an english category label which represent a red green or blue colour channel.

Rotobot Segmentation
^^^^^^^^^^^^^^^^^^^^

Pixels that belong to that category's semantic label will be active in the colour channel you choose.

For example, if you choose red for cat you will get a red coloured mask shaped in the siloquette of a cat, if there is a cat in your image.

Without ticking any boxes automatic colours will be chosen for you, which are hard coded into Rotobot.

Rotobot Instance Segmentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A pixel coordinate may be given to isolate pixel belonging to an indivdual detection of a instance of a category.

By default these pixel coordinates are negative and will match all instances.

When you give a pixel coordinate you only get the ``cat`` under this pixel coordinate.

Using expressions and pixel tracking you can isolate in individual from a group.

Rotobot Trimap
^^^^^^^^^^^^^^

A three colour alpha transperancy channel can be improved from black for background, white for foreground and other greys will be determined by the deep learning model.

The improvement from a trimap hint alpha transperancy is that the resulting alpha transperancy channel has been trained to know what semi transperant edges should look like.

The smaller the undetermined grey area is the less ambiguity for the deep learning model.

Input and Output are RGB and RGBA
=================================

The following nodes expect a 32 bit per pixel RGB input and will return an RGB output

#. Rotobot Instance Segmenation
#. Rotobot Segmentation

To use the result to make an alpha transperancy, a user can shuffle the channels used into the alpha channel

The following nodes expect a 32 bit per pixel RGBA input and will return a RGBA output

#. Rotobot Trimap


.. `input_colorspace`

Input Colorspace
================

It is expected that a neutral grey will be represented as 0.5 to all Rotobot Nodes.

If your footage is in ACEScg a neutral grey will have a value closer to 0.2

For this reason, if you use an OCIO Color Transform Node to compute an sRGB or rec709 Display LUT into the pixels.

In this way you can convert a ACEScg Scene Linear image to a sRGB Display Image.

A good test is to compare the image of an image from the Internet such as a PNG or JPEG image with no colour managment to your input to a Rotobot node, they should have a comparable look.


Create a mask using Rotobot Segmentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Prepare your input image to be a resolution less than 2049 pixels in the maximum width, larger will not cause an error.
2. Ensure your input is in the appropriate colour space for Rotobot see `Input Colorspace`_.
3. Create a Rotobot Segmentation Node
4. Choose the category ``cat`` for example in the red group section, if you have a cat visible in your image
5. Connect the input node to the Rotobot Segmentation Node
6. View the output of the node
7. Computation will start, the deep learning computer vision model will be decrypted and transferred to the GPU if available.
8. Allow for up to 40 seconds for the computation to start, the computation may take less than a second or up to several minutes per frame depending on hardware.
9. Pixels that belong to the category you have chosen will be highlighted in red.
10. Using your compositing package you can use the red channel as an alpha mask to create a video layer.

Isolate and seperate an indivdual using Rotobot Instance Segmentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Prepare your input image to be a resolution less than 2049 pixels in the maximum width, larger will not cause an error.
2. Ensure your input is in the appropriate colour space for Rotobot see `Input Colorspace`_.
3. Create a Rotobot Segmentation Node
4. Choose the category ``cat`` for example in the red group section, if you have a number of cats visible in your image
5. Connect the input node to the Rotobot Instance Segmentation Node
6. View the output of the node
7. Computation will start, the deep learning computer vision model will be decrypted and transferred to the GPU if available.
8. Allow for up to 40 seconds for the computation to start, the computation may take less than a second or up to several minutes per frame depending on hardware.
9. Pixels that belong to the category you have chosen will be highlighted in red, for all of the detections
10. Using your cursor, note the pixel coordinate over one of the cats in your image, for instance ``X: 900`` and ``Y: 270``
11. Change the default X and Y coordinates from the value of ``X: -1`` and ``Y: -1`` to the coordinate you detemined above
12. Now only the instance of the category cat under the pixel coordinates will be highlighted
13. Using your compositing package you can use the red channel as an alpha mask to create a video layer.

Create a soft mask using Trimap
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Prepare your input image to be a resolution less than 2049 pixels in the maximum width, larger will not cause an error.
2. Ensure your input is in the appropriate colour space for Rotobot see `Input Colorspace`_.
3. Create a Rotobot Segmentation Node
4. Choose the category ``cat`` for example in the red group section, if you have a cat visible in your image
5. Connect the input node to the Rotobot Segmentation Node
6. View the output of the node
7. Computation will start, the deep learning computer vision model will be decrypted and transferred to the GPU if available.
8. Allow for up to 40 seconds for the computation to start, the computation may take less than a second or up to several minutes per frame depending on hardware.
9. Pixels that belong to the category you have chosen will be highlighted in red.
10. Using filters to grow and shrink the edge of the detection, you can make three zones in your image.
11. White 1.0 is where you are certain it will be foreground.
12. Black 0.0 is where you are certain it will be background.
13. Grey 0.5 is where you want the deep learning model to approximate the edge on your behalf.
14. When you have a channel prepared that meets the above criteria, using the composting tools make it the alpha channel of an input
15. The RGB of this input needs to be in the colour space described in `Input Colorspace`_, the A of the RGBA needs be be 0.0, 0.5 or 1.0
16. Using a filter to limit the alpha channel input to three colours works well.
17. Connect the RGBA image to a newly created Rotobot Trimap node.
18. Use the channel tools to inspect the output A of the resulting RGBA, it will have values updated from the input.
19. Use your compositing tools to use this alpha mask to create a video layer.

