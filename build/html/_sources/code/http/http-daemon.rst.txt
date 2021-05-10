Using HTTP Daemons for Resourcepacks
====================================

While resourcepacks allow players to hear custom sounds, you cannot
simply send them using a file. You must used a direct link to the
zip file. One solution to solve this is by using an HTTP file server
to host the pack for users.

.. note::
  For more information about resourcepack wrappers, visit:

  .. toctree::

      ../resourcepack/wrapper

This assumes that you already properly wrapped the resourcepack and
completed the necessary requirements to build the file.

Creating a HTTP Daemon
----------------------

Creating a HTTP Daemon is as easy as instantiating the
`HTTPDaemonProvider <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/681e74d318591283d7059d1f9de631999ab42cea/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/resourcepack/hosting/HttpDaemonProvider.java>`__
class. The daemon requires only two arguments. A path and a port.

The path is the place where the root of the HTTP server will be
located. This is also where users can find and download files
from the server.

.. warning::
  Do not set this directory to any private files! Only set it to
  an empty, unused folder. MinecraftMediaLibrary automatically
  handles it such that requests cannot access files outside the
  specified root folder, but does not block requests which access
  anything inside the folder!

The port is a specified integer that will be used to host the
daemon on. This port must be open, properly port-forwarded with
your router, and available for use.

The class also provides methods to start the server, generate a
link to a specific file (inside the HttpDaemonProvider), and
also retrieving the public IP of the server.

As for code examples, here is a example piece of code for using
this class.

.. code:: java

  /*

  This specifies a HTTP server with the root folder set to
  "C://http", and a port set to 2020.

  */
  final HttpDaemonProvider provider = new HttpDaemonProvider("C://http", 2020)

  // Starts the HTTP server
  provider.startServer();

  // Generates a url with the specified path (http:://[PUBLIC_IP]:[PUBLIC_PORT]/resourcepack.zip)
  final String url = provider.generateUrl(Paths.get("C://http/resourcepack.zip"));

And that's it! Use the generated links to provider users with the
necessary files they need to download.
