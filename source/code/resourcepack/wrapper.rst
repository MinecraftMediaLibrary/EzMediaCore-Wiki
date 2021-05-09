Using a Resourcepack Wrapper
============================

Wrapping a resourcepack is not easy as you need to make sure
to place all the files in the correct areas.

.. note::
  For more information about resourcepacks, visit:

  .. toctree::

      ../../../resourcepack

The resourcepack wrapper in MinecraftMediaLibrary's case uses
sound to be wrapped.

Creating a Resourcepack Wrapper
-------------------------------

To create a resourcepack wrapper, we will be using the
`ResourcepackWrapper <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/resourcepack/ResourcepackWrapper.java>`__
class. It requires an instance of the library, a path to which the
resourcepack should be built, a path to the audio, a path to the icon
(set to null if you don't want one), a description, and a packFormat.

The audio should be a path to an ogg file. The icon file should lead to
a png file named "pack.png". The description should be a non-null description
that can be empty. Finally, the packFormat is a format used to set the version
of the pack that should be used (which varies per Minecraft version). Also,
there is a builder that can be used to assist with this.

.. code:: java
  /*

  setPath("C://resourcepack.zip") -> Sets output path of resourcepack.

  setDescription("Example Resourcepack") -> Sets description of resourcepack.

  setAudio("C://audio.ogg") -> Sets audio to the ogg file.

  setIcon("C://pack.png") -> Sets icon to the png file.

  setPackFormat(6) -> Sets the pack-format to 6 (1.16).

  */

  final MinecraftMediaLibrary library = ...;

  final ResourcepackWrapper wrapper =
    ResourcepackWrapper.builder()
      .setPath("C://resourcepack.zip")
      .setDescription("Example Resourcepack")
      .setAudio("C://audio.ogg")
      .setIcon("C://pack.png")
      .setPackFormat(6)
      .build(library);

MinecraftMediaLibrary allows you to also convert a YoutubeExtraction (explained in
the extraction section) to a ResourcepackWrapper if necessary. Just use the
`ResourcepackWrapper#of` method. The method also accepts a sound for a prebuilt
pack if you are lazy.

.. code:: java
  final ResourcepackWrapper wrapper = ResourcepackWrapper.of(extractor, library);

Building the Resourcepack
-------------------------

After creating the ResourcepackWrapper, call the `buildResourcePack()` method to
build the resourcepack at the target folder.

Method Events
-------------

When creating a ResourcepackWrapper, you may override the `onResourcepackBuild()`
method to be called right before the pack is created. Note however that you cannot
use the builder and must use the constructor (for anonymous class definition).

  
