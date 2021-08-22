Instantiating Audio Attributes
==============================

To instantiate an AudioAttributes, you need four arguments.

You need a `bitrate <https://en.wikipedia.org/wiki/Bit_rate#Audio>`__
, a number of `channels <https://en.wikipedia.org/wiki/Surround_sound>`__
, a `sampling rate <https://en.wikipedia.org/wiki/Sampling_(signal_processing)>`__
, and a `sound volume <https://en.wikipedia.org/wiki/Loudness>`__.

The bitrate, channels, and sampling rate should all be above 0.

The volume, however, can be 0 (to mute it). Otherwise, it also follows
the requirement that it must be greater or equal to 0.

.. note::
  The bitrate unit is set to bits per second. This means that you should
  set it to something like 160,000 bits per second (for 160 kbps) and not
  160!

  Channels should only be set to 1 or 2.

  Finally, the sampling rate is set in hertz. So if you wanted to set the
  audio for 44.1 kHz, use 44,100, and not 44.1!

.. code-block:: java

  /*

  "ogg" -> Codec of the Audio
  160_000 -> Bitrate of Audio
  1 -> Channels for Audio
  44_100 -> Sampling Rate of Audio
  50 -> Volume of Audio

  */
  final AudioAttributes attributes = new AudioAttributes("ogg", 160_000, 1, 44_100, 50);
