Support for Linux (Extremely Hard)
==============================================================

.. image:: https://icons.iconarchive.com/icons/tatice/operating-systems/256/Linux-icon.png

Support for Linux will be extremely hard. The difference between Linux and Windows/Mac wasn't just architectures,
but also due to the different binaries for each Linux distribution.

I originally created a huge list of URLs to mirrors for Linux packages for different operating systems (and even
hosted one on Github myself `right here <https://github.com/MinecraftMediaLibrary/VLC-Release-Mirror/tree/master/linux>`__)
however, newer problems arose.

As you probably know, Linux uses packages to install software. These packages come in various types, such as tgz, txz,
deb, rpm, etc. Packages such as tgz and txz already have binaries, meaning it is no problem with them. However, two
types of packages (DEB and RPM) do not contain the binaries but rather information about the package. It forces the
user to run a command (`sudo apt-install`) or some similar command to install the package. You may ask, why can't I
just run that command and I should be fine... right?

Nope. Notice the keyword `sudo` inside there. Sudo requires either the user to be root or else it requires a password
that you must enter after. This is not ideal because on shared server hosting (such as BisectHosting, Minehut, etc), I
doubt the server provider will give you the password or root. The solution was to install the package without root, and...
it isn't easy.

One proposed solution I had was about using `JuNest <https://github.com/fsquillace/junest>`__. However, it lead to many problems
such as restrictions in the OS, the app itself actually needing to download certain dependencies before being able to run, etc.
It posed multiple restrictions.

Another solution was to use Snap. However, installing Snap requires sudo, which puts us back into a loophole!

My last resort was to download the binaries off from VLC and compile them using the gcc command. However, this obviously requires
the gcc command to be installed which leads to many other problems too (not all distributions have it pre-installed, and I doubt
a server like BisectHosting would have that installed).

Currently, I am stuck. I have no idea of any solutions to possibly solve this. I went as far as using Conda for a possible
solution but they just led to more and more problems. If you have a suggestion, feel free to tell me. This also means that
support for Linux is not available at the moment. If you want to see my thoughts on how I tried to pull out some algorithm,
take a look
`here <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/2c80ff5441e2108fba6e365dd0709ac95a122713/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/vlc/os/linux/pkg/PackageBase.java#L36>`__
