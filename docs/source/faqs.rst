Frequenty Asked Questions (FAQs)
================================

How accurate is Rotobot?
^^^^^^^^^^^^^^^^^^^^^^^^

It depends…

Rotobot Instance Segmentation is very inaccurate when the category detected is large in screen size, Rotobot Segmentation is more accurate but more expensive to calculate, Rotobot Trimap can give soft edges and is even more expensive to calculate. None of the above is a replacement for hours of hand Rotoscoping getting a perfect edge. It is intended as a place holder so you can get started and see what needs to be improved. Rotobot makes pixel based masks rather than splines that can be adjusted and animated by changing a small number of animated keyframe values, to improve on Rotobot mask you will need to use paint techniques.

Why is it so slow?
^^^^^^^^^^^^^^^^^^

Deep Neural networks are large computations. If you have ever created a blur operation, you will know the larger the blur amount the longer it will take to compute. The calculations in a convolutional neural network do the equivalent computation of many many blur operations. These computations are stored as variables of the deep learning model that has trained for days on a large pool of data on some specialised hardware. Often the first frame of computation will need to load this model up and present it to the computer or the computer’s graphic’s card so the first initialisation will have some “spin up time”. After the first frame subsequent frames will take less time. So if you need to choose a batch size of how many frames to compute before starting the program again, choose a larger batch size, so you can spread the “spin up time” across the cost of the batch of frames. Similarly if you swap between one node and another, this moving memory from one place to another can be inefficient, if you can compute and write to disk and then look up the disk result, things will be faster overall, rather than connecting results from volatile memory.

What is the colour space to get the best detection?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Assuming your are compositing in a scene linear colour space such as ACEScg.

As a rule of thumb, if your image looks pale with the lookup table and looks natural without the lookup table, this is the expected input Rotobot detection for a Display sRGB image.

So pixel values for a neutral grey will be approximately 0.5.
 
Why does my 5K image take so long?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The internals of the current version of Rotobot only support images of less than 2049 x 2049. It will be interpolated back to the input resolution but no additional detail will be added. A better approach would be to scale your image down to approximately 1080p use Rotobot and then resize the result.

How do I install Rotobot?
^^^^^^^^^^^^^^^^^^^^^^^^^

Installing Rotobot is a matter of putting your details into the web store and choosing the appropriate installer. You will receive an email with the download details. If you use a “ten minute email” you are in violation of the end user license agreement. You will be unable to gain a trial license to remove the watermark.

Once you have downloaded the product, administrator rights are required for a simple installation, advanced installation can be done without administrator privileges and will require reading of the System Administrator docs.

There are few choices to make during the installation apart from the location where you would like to put the software, the default location makes sense in most situations.

Please read the End User License Agreement because by installing the software you are entering into an agreement with Kognat Pty. Ltd. that is legally binding.

What is that glitch?
^^^^^^^^^^^^^^^^^^^^

The watermark will appear and checkers and random brightly coloured squares, these are not GPU artefacts but intellectual copyright protection.

Purchase of a license will remove the watermark

How do I install a license?
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please see the System Administrator notes.

Kognat staff are in the process of simplifying the process, soon installing a license will be as easy as downloading a license installer and running the installer. But as there are both node locked licenses and client-server based floating license. The answer to “How do I install a license?” is “It depends on the license you are installing and your operating system”

Be patient while we support your needs and level of aptitude with your operating system and complexity of your studio’s needs. 

