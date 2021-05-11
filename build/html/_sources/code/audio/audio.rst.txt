Creating an Audio Player
========================

Creating an audio player is relatively easy using the MinecraftMediaLibrary
api. You may extract the audio from a Youtube link or use an .ogg file for
doing this. Create a
`Resourcepack Wrapper <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/resourcepack/ResourcepackWrapper.java>`__
off of this, and host it using either by manually doing it or by an HTTP
server (which the library supports).

.. note::
  For more information about Resourcepack Wrappers, visit

  .. toctree::

      ../resourcepack/wrapper

When using a Youtube link, define a new
`YoutubeExtraction <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/extractor/YoutubeExtraction.java>`__.

.. note::
  For more information about Youtube Extractors, visit

  .. toctree::

      ../youtube/youtube-extraction

The hyperlinks will show you how to create the resourcepack.

Playing the Actual Audio
------------------------

To play the actual audio, you would have to call the sound name that
is your plugin name to full lowercase. Getting the plugin name is
equivalent to Plugin#getName.

As for doing this in Spigot specifically, just use the playSound
method part of the Player class or World class to play the specific
sound so entities can hear it.

Example for playing the sound in a World:

.. code-block:: java

  final Plugin plugin = ...;
  final World world = Bukkit.getWorld("world");
  world.playSound(new Location(world, 0, 0, 0), plugin.getName().toLowerCase(), 1.0F, 1.0F);

Example for playing the sound for a specific Player:

.. code-block:: java

  final Plugin plugin = ...;
  final World world = Bukkit.getWorld("world");
  final Player player = Bukkit.getPlayer("PulseBeat_02");
  player.playSound(player.getLocation(), plugin.getName().toLowerCase(), 1.0F, 1.0F);
