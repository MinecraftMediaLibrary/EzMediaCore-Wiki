Loading VLC Binaries on Windows
===============================

.. image:: ../../resources/images/windows-icon.png
  :width: 256

Windows uses .DLL extensions. When we find the plugin path folder,
it is automatically set to the same path (no need for any relative
paths). Due to Windows binaries being set mainly in the root
directory, I have disabled heuristics as it is not necessary.
