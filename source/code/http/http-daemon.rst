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
`HTTPServer <https://github.com/MinecraftMediaLibrary/EzMediaCore/blob/master/main/src/main/java/io/github/pulsebeat02/ezmediacore/resourcepack/hosting/HttpServer.java>`__
class. The daemon requires mainly two arguments. A path and a port.

The path is the place where the root of the HTTP server will be
located. This is also where users can find and download files
from the server.

If you pass in an instance of the library instead for the first
argument, it will instead use the library's http server folder
provided.

.. warning::
  Do not set this directory to any private files! Only set it to
  an empty, unused folder. EzMediaCore automatically
  handles it such that requests cannot access files outside the
  specified root folder, but does not block requests which access
  anything inside the folder!

The port is a specified integer that will be used to host the
daemon on. This port must be open, properly port-forwarded with
your router, and available for use.

The class also provides methods to start the server, generate a
link to a specific file, and also retrieving the public IP of the
server.

As for code examples, here is a example piece of code for using
this class.

.. code:: java

  /*

  This specifies a HTTP server with the root folder set to
  "C://http", and a port set to 2021.

  */
  final HttpServer server = new HttpServer(Path.of("C://http"), 2021)

  // Starts the HTTP server
  server.startServer();

  // Generates a url with the specified path (http:://[PUBLIC_IP]:[PUBLIC_PORT]/resourcepack.zip)
  final String url = provider.generateUrl(Path.of("C://http/resourcepack.zip"));

  // Stops the HTTP server
  server.stopServer();

And that's it! Use the generated links to provider users with the
necessary files they need to download.
