MinecraftMediaLibrary General Information
=========================================

This section is intended for developers and **strongly** recommended for readers to take
a look at if they want to use the library and know what is going on internally.

VLC Media Player
----------------

.. image:: ../resources/images/vlc.svg
  :width: 256

The library uses a very common media player today known as
`VLC Media Player <https://www.videolan.org/>`__. The reason due to this is because
of how efficient the program is to provide callbacks to actual frames in production
code. It is able to read an MPEG file and many other video formats allowing it to be
flexible, and a very much valid option to choose.

.. note::
  Frame callbacks (as described above) are callbacks where an external library or API
  sends frame data to your own consumer, allowing you to process the data if necessary.
  In this case, VLC Media Player is used to send frame data from the MPEG video into
  our application, which allows easier processing and faster video data retrieval (due
  to how it is written in C/C++/Lua).

Implementing VLC Into MinecraftMediaLibrary
-------------------------------------------

Obviously, VLC Media Player is not written in Java, but mainly composed in C, C++, and
other native libraries. Luckily, a project known as `VLCJ <https://github.com/caprica/vlcj>`__
which provides bindings and a functional API to provide callbacks into Java code.

.. warning::
   While VLCJ is able to provide us with built in video players, there are some drawbacks.
   For example, VLCJ is not suitable for multiple players at once! Take a look at
   `this post <https://capricasoftware.co.uk/projects/vlcj-pro>`__ about how the creator
   of VLCJ (Caprica) attempts to solve this issue by creating "Out of Process" media players.
   To sum up, some of the libraries VLC uses are not thread-safe and reentrant, causing them
   to create fatal crashes. This means multiple concurrent threads (or video players) accessing
   such native libraries will likely be unsafe.

Due to such restrictions, MinecraftMediaLibrary as in the current patch does not support multiple
video playback at once. It is unsafe and not ready for production. However, in the near future,
perhaps VLCJ - Pro could be an option.

Handling VLC Binaries
---------------------

This is arguably one of the hardest problems I had to solve -- giving support to multiple platforms.
Not everyone will have VLC installed on their PC. I had to find a way to fix or bypass this issue.
Unfortunately, VLC uses binaries that are dependent on the Operating System of the environment. This
means that Windows, Mac, Linux (and even separate Linux Distributions) have their own binaries to use.

.. note::
  For information about how I implemented a solution to install the binaries for the users, take a look
  below.

  .. toctree::
     :maxdepth: 1

    binaries/windows-installation
    binaries/mac-installation
    binaries/linux-installation

Loading VLC Binaries
--------------------

Loading VLC binaries is a separate issue as each operating system requires it's own method of loading the
VLC binaries. After installing the binaries for the user, we must load them properly in order for the
library to use them properly.

.. note::
  VLCJ provides a great strategy for loading called
  `NativeDiscovery <http://caprica.github.io/vlcj/javadoc/4.0.4/uk/co/caprica/vlcj/factory/discovery/NativeDiscovery.html>`__
  however, due to how Minecraft servers function, this method will not work.

To go into more detail on why NativeDiscovery does not work, the method uses
`ServiceLoader <https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html>`__ to find and load
the possible directories. The class which uses ServiceLoader can be found
`here <http://caprica.github.io/vlcj/javadoc/4.0.7/uk/co/caprica/vlcj/factory/discovery/provider/DirectoryProviderDiscoveryStrategy.html>`__.
According to StackOverflow, ServiceLoader will only find certain classes loaded by the current classloader thread. After
a load of debugging, I've finally found that due to how the Minecraft server is running on a different classloader thread
from the actual library, it can find the proper paths. Thus, I had to implement my own mini-NativeDiscovery implementation
to try and load VLC.

Implementing My Own Solution for NativeDiscovery
------------------------------------------------

I created separate abstractions for each module. In order to load VLC binaries, I created a method which takes in
a directory and attempts to load VLC from that directory. It uses recursion to locate the plugins folder and the folder
containing core libraries of VLC (such as libvlc, libvlccore, etc). The strategy/algorithm can be found
`here <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/2c80ff5441e2108fba6e365dd0709ac95a122713/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/vlc/os/MMLNativeDiscovery.java#L69>`__.

It first tries to identify if NativeDiscovery works on the system or not (which we know doesn't work, but maybe it will work
some day!). Then, I used a heuristic algorithm to improve the search. I added keywords that sort the PriorityQueue such that
files with the keyword would appear at the top, improving overall speed.

Once I found the plugins folder, I set the VLC plugin path relative to that. It sets an enviornment variable that VLC can use.
If I found the native library, I also set that up too. Each operating system has it's own relative paths to set for environment
variables and VLC path.

.. note::
  For more information about how I loaded each of the binaries for the Operating Systems, take a look at the links below.

  .. toctree::
     :maxdepth: 1

    load/windows-load
    load/mac-load
    load/linux-load
