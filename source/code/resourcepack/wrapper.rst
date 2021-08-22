Using a Resourcepack Wrapper
============================

Wrapping a resourcepack is not easy as you need to make sure
to place all the files in the correct areas.

.. note::
  For more information about resourcepacks, visit:

  .. toctree::

      ../../../resourcepack

The resourcepack wrapper in EzMediaCore's case uses
sound to be wrapped.

Creating a Resourcepack Wrapper
-------------------------------

To create a resourcepack wrapper, we will be using the
`ResourcepackWrapper <https://github.com/MinecraftMediaLibrary/EzMediaCore/blob/master/main/src/main/java/io/github/pulsebeat02/ezmediacore/resourcepack/ResourcepackWrapper.java>`__
class. It requires an instance of the library, a path to which the
resourcepack should be built, a path to the audio, a path to the icon
(set to null if you don't want one), a description, and a packFormat.

The audio should be a path to an ogg file. The icon file should lead to
a png file named "pack.png". The description should be a non-null description
that can be empty. Finally, the packFormat is a format used to set the version
of the pack that should be used (which varies per Minecraft version). Also,
there is a builder that can be used to assist with this.

.. code-block:: java
  /*

  "C://example.zip" -> Target of resourcepack file
  "Example Resourcepack" -> Description of resourcepack file
  6 -> Format of resourcepack file
  "C://icon.png" -> Icon image for resourcepack (must be 128x128 and png file)
  The icon is an optional argument.

  */

  final ResourcepackWrapper wrapper = new ResourcepackWrapper(
    Path.of("C://example.zip"),
    "Example Resourcepack",
    6,
    Path.of("C://icon.png"));

EzMediaCore allows you to also convert a YoutubeExtraction (explained in
the extraction section) to a ResourcepackWrapper if necessary. Just use the
`ResourcepackWrapper#of` method. The method also accepts a sound for a prebuilt
pack if you are lazy.

Adding Files to the Resourcepack
--------------------------------

.. code-block:: java
  /*

  "assets/blocks/textures/example-texture.png" -> Adds the file to the specific
  location relative to the resourcepack root folder.
  "C://my-texture.png" -> The file to add.

  */
  wrapper.addFile("assets/blocks/textures/example-texture.png", Path.of("C://my-texture.png"))

You may also pass a byte[] as the second argument if you want to declare the
specific bytes to use for the file.

Removing Files from the Resourcepack
------------------------------------

.. code-block:: java
  /*

  "assets/blocks/textures/example-texture.png" -> Removes the specific file
  relative to the location of the resourcepack root folder.

  */
  wrapper.removeFile("assets/blocks/textures/example-texture.png")

Building the Resourcepack
-------------------------

After creating the ResourcepackWrapper, call the `wrap()` method to
build the resourcepack at the target folder.

Resourcepack Wrap Events
------------------------

When creating a ResourcepackWrapper, you may override the `onPackStartWrap()`
method to be called right before the pack is created, or `onPackFinishWrap()`
which would be called after the pack has been created.
