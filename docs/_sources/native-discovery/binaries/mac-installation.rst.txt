Support for Mac (Medium)
==============================================================

.. image:: https://cdn2.iconfinder.com/data/icons/social-icons-color/512/apple-512.png

Support for Mac is similar to support on Windows, however, it is a bit harder. Mac OS systems store their
apps in folders with a .APP extension, but are still folders. For example, if you had Chrome as an app,
the application folder would be named "Chrome.APP", and will have a folder of contents used to run the
software. The same goes with VLC Media Player. However, I encountered an issue that I couldn't simply
just zip up the folder for the application contents. Mac has this odd hash or certificate check which
didn't allow the user to run/use the app even if the folder was named .APP and had non-corrupted contents.

Instead, I had to resort to DMGs or disk files on Mac. I would run a native command to mount the disk file
onto the PC. Then, I recursively copied the folder contents of the VLC app over to the dependency folder.
That way, the operating system was able to identify the app as valid and allowed execution/use of the binaries
and app itself.

I uploaded the DMGs onto Github as a mirror for users to download. Unlike Windows which had 32-bit and 64-bit,
most Mac Systems these days are 64-bit. Instead, I provided two versions — arm64 and intel64 because the binaries
of these architectures were different.

`ARM64 Version <https://github.com/MinecraftMediaLibrary/VLC-Release-Mirror/tree/master/macos-arm64>`_

`INTEL64 Version <https://github.com/MinecraftMediaLibrary/VLC-Release-Mirror/tree/master/macos-intel64>`_

Currently, MinecraftMediaLibrary supports Mac. There are no plans for removing support in the near future.
