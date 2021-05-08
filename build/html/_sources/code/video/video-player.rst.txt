Introduction to Video Players
=============================

Video Players in MinecraftMediaLibrary are one of the most powerful features
in the library.

In the library, we differentiate two parts of a video player. The **frame callback**
part and the **video player component** part.

The frame callback acts as a callback handler from frames passed from VLC to provide
the necessary dithering/setup needed to process the frame. All frame callbacks implement
the
`FrameCallback <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/frame/FrameCallback.java>`__
class.

.. note::
  Dithering is the process of downscaling certain RGB colors from a palette. There are
  multiple algorithms for dithering such as linear/ordered dithering and error diffusion
  dithering (which adds some spaces in between the dithered colors), but that is the basic
  idea.

The video player component acts as the video player and provides certain features such
as an audio play button, a pause button, a resume button, a release button, etc. All
video players extend the
`VideoPlayer <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/frame/VideoPlayer.java>`__
class.

.. note::

   A frame callback and video player must have the correct parts associated with each other.
   This describes the correct classes to be used with each other.

   +------------------------+-----------------------------+
   | **Frame Callback**     | **Video Player**            |
   +------------------------+-----------------------------+
   | MapDataCallback        | MapIntegratedPlayer         |
   +------------------------+-----------------------------+
   | ChatCallback           | ChatIntegratedPlayer        |
   +------------------------+-----------------------------+
   | EntityCloudCallback    | EntityCloudIntegratedPlayer |
   +------------------------+-----------------------------+
   | BlockHighlightCallback | BlockHighlightPlayer        |
   +------------------------+-----------------------------+
   | ScoreboardCallback     | ScoreboardIntegratedPlayer  |
   +------------------------+-----------------------------+

   **Experimental Players:** (work in progress, not ready for use)

   +------------------------+-----------------------------+
   | **Frame Callback**     | **Video Player**            |
   +------------------------+-----------------------------+
   |                        | GifIntegratedPlayer         |
   +------------------------+-----------------------------+
   |                        | ParallelVideoPlayer         |
   +------------------------+-----------------------------+

   .. toctree::

       maps
       entities
