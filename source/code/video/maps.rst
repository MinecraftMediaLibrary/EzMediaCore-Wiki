Map Video Players
=================

Map Video Players, as the name stands, are videos that are played
on maps. Maps are displayable on itemframes, meaning that players
are able to place itemframes on certain blocks, set the maps onto
them, and watch video playback then.

.. note::
  For more information about maps, visit the following:

  .. toctree::

      ../../../map

Maps are very great at delivering videos. Their quality from dithering
is considered even better than the quality used for entity name tags
even though they have limited color. Dithering allows for this magic
to happen.

When retreiving a map in normal Minecraft, typically one would type
the following command:

.. code-block::

  /give @p filled_map{map:[id]}

Replace [id] with the specific map id you would like to retreive. For
example, getting a map with id 0 would be the following:

.. code-block::

  /give @p filled_map{map:0}

Creating a Map Callback
-----------------------

As for any video player, you must specific the callback that the video
player will use. To do this, we will use the
`MapDataCallback <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/frame/map/MapDataCallback.java>`__
class. To initialize the class, it requires an instance of our library,
the viewers, the itemframe width/height, the video width (in pixels),
the first map to use, and the delay between frames. A builder is
provided for easier use.

.. code-block:: java

  /*

  Suppose we wanted to play a video on a 5x5 itemframe screen.
  The video has a width in pixels of 640 pixels.

  setViewers(null) -> Set to null for everybody. Otherwise set
  to the viewers that see the video

  setMap(0) -> Set the base map. In this case, we are using 5x5
  itemframes, so we have 25 itemframes or 25 maps. That means
  that the ids occupied will be set from 0 - 24 (25 possible
  maps).

  setItemframeWidth(5) -> Sets the itemframe width to 5 blocks.

  setItemframeHeight(5) -> Sets the itemframe height to 5 blocks.

  setVideoWidth(640) -> Sets the video width to 640 pixels.

  setDelay(0) -> Sets the delay between each frame to be 0 milliseconds.

  setDitherHolder(new FilterLiteDither()) -> Sets the dithering algorithm to
  be Filter Lite algorithm. For a list of algorithms please look at the
  dithering documentation.

  */
  final MinecraftMediaLibrary library = ...;

  final MapDataCallback callback =
    MapDataCallback.builder()
      .setViewers(null)
      .setMap(0)
      .setItemframeWidth(5)
      .setItemframeHeight(5)
      .setVideoWidth(640)
      .setDelay(0)
      .setDitherHolder(new FilterLiteDither())
      .build(library);

Once we are done creating the callback, we can now try and create the actual
video player!

Creating a Map Video Player
---------------------------

Now that we created our callback, we can use that to create our video player.
We will use the
`MapIntegratedPlayer <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/frame/map/MapIntegratedPlayer.java>`__
for this. To instantiate this class, we will just pass in a
library instance, a url to the media (can be Youtube or a File),
the callback we defined before, and also the width/height of the video.
Take a look at this example:

.. code-block:: java

  final MinecraftMediaLibrary library = ...;

  final MapDataCallback callback =
    MapDataCallback.builder()
      .setViewers(null)
      .setMap(0)
      .setItemframeWidth(5)
      .setItemframeHeight(5)
      .setVideoWidth(640)
      .setDelay(0)
      .setDitherHolder(new FilterLiteDither())
      .build(library);

  /*

  Using the example above, assume our video is located in
  C://video.mp4 and has a width of 640 pixels, and height of
  480 pixels.

  setUrl("C://video.mp4") -> Sets the mrl to be the path of the video.

  setCallback(callback) -> Sets the callback for the video player.

  setWidth(640) -> Sets the width to be 640 pixels.

  setHeight(480) -> Sets the height to be 480 pixels.

  */
  final MapIntegratedPlayer player =
    MapIntegratedPlayer.builder()
      .setUrl("C://video.mp4")
      .setCallback(callback)
      .setWidth(640)
      .setHeight(480)
      .build(library);

After that, we are done! Just use the control methods on the video to
play, pause, or release.
