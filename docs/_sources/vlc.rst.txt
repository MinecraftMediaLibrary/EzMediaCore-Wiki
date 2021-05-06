MinecraftMediaLibrary and VLC Media Player
==============================================================

This section is intended for developers and **strongly** recommended for readers to take
a look at if they want to use the library and know what is going on internally.

What is VLC Media Player?
==============================================================

.. image:: https://images.videolan.org/images/icons-VLC/vlc.mini.svg
  :width: 200

The library uses a very common media player today known as
`VLC Media Player <https://www.videolan.org/>`_. The reason due to this is because
of how efficient the program is to provide callbacks to actual frames in production
code. It is able to read an MPEG file and many other video formats allowing it to be
flexible, and a very much valid option to choose.

.. note::
  Frame callbacks (as described above) are callbacks where an external library or API
  sends frame data to your own consumer, allowing you to process the data if necessary.
  In this case, VLC Media Player is used to send frame data from the MPEG video into
  our application, which allows easier processing and faster video data retrieval (due
  to how it is written in C/C++/Lua).

How Does MinecraftMediaLibrary Use VLC Media Player?
==============================================================

Obviously, VLC Media Player is not written in Java, but mainly composed in C, C++, and
other native libraries. Luckily, a project known as `VLCJ <https://github.com/caprica/vlcj>`_
which provides bindings and a functional API to provide callbacks into Java code.

.. warning::
   While VLCJ is able to provide us with built in video players, there are some drawbacks.
   For example, VLCJ is not suitable for multiple players at once! Take a look at
   `this post <https://capricasoftware.co.uk/projects/vlcj-pro>`_ about how the creator
   of VLCJ (Caprica) attempts to solve this issue by creating "Out of Process" media players.
   To sum up, some of the libraries VLC uses are not thread-safe and reentrant, causing them
   to create fatal crashes. This means multiple concurrent threads (or video players) accessing
   such native libraries will likely be unsafe.

Due to such restrictions, MinecraftMediaLibrary as in the current patch does not support multiple
video playback at once. It is unsafe and not ready for production. However, in the near future,
perhaps VLCJ - Pro could be an option.

Great, But VLC Uses Binaries Right?
==============================================================

This is arguably one of the hardest problems I had to solve -- giving support to multiple platforms.
Not everyone will have VLC installed on their PC. I had to find a way to fix or bypass this issue.
Unfortunately, VLC uses binaries that are dependent on the Operating System of the environment. This
means that Windows, Mac, Linux (and even separate Linux Distributions) have their own binaries to use.

For information about how I implemented a solution to install the binaries for the users, take a look
below.

Links to Sections
==============================================================

.. toctree::
   :maxdepth: 2

   native-discovery/binaries/windows-installation
   native-discovery/binaries/mac-installation
   native-discovery/binaries/linux-installation


VLCJ provides a great strategy for loading called
`NativeDiscovery <http://caprica.github.io/vlcj/javadoc/4.0.4/uk/co/caprica/vlcj/factory/discovery/NativeDiscovery.html>`_
however I will explain why NativeDiscovery will not work for the scope of Minecraft Servers.
