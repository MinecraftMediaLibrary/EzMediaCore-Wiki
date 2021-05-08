Retrieving Video/Audio from Youtube Videos
==========================================

MinecraftMediaLibrary provides an easy way to extract video and audio
from an existing Youtube link. This Youtube link can be either public or
unlisted.

To start off, we will be using the
`YoutubeExtraction <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/extractor/YoutubeExtraction.java>`__
class. To instantiate one, we need three parameters: A URL directly to
the Youtube Link, a directory to download the files, and an
`ExtractionSetting <https://github.com/MinecraftMediaLibrary/MinecraftMediaLibrary/blob/master/minecraftmedialibrary-api/src/main/java/com/github/pulsebeat02/minecraftmedialibrary/extractor/ExtractionSetting.java>`__

.. note::
  The Youtube link can be formatted in anyway such that the Youtube id is
  visible. In most cases, just copying the link (and it can be any format)
  will be fine. MinecraftMediaLibrary is able to handle and extract the ids
  accordingly.

The Youtube URL is the link to the Youtube video.

The directory is the directory for which the video and audio files should be stored.

And finally the ExtractionSetting is a set of attributes that MinecraftMediaLibrary
will use when extracting audio.

.. note::
  For more information about instantiating an ExtractionSetting, take a look at:

  .. toctree::

    extraction-setting

As for an example of instantiating a new YoutubeExtraction, take a look at this
code snippet:

.. code-block:: java

  /*

  160_000 -> Bitrate of Audio
  1 -> Channels for Audio
  44_100 -> Sampling Rate of Audio
  50 -> Volume of Audio

  */
  final ExtractionSetting setting = new ExtractionSetting(160_000, 1, 44_100, 50);

  /*

  "https://www.youtube.com/watch?v=dQw4w9WgXcQ" -> Youtube Link
  "C://video" -> Path to Directory
  settings -> Extraction Settings (defined above)

  */
  final YoutubeExtraction extractor = new YoutubeExtraction(
    "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
    "C://video",
    settings
  );

Extracting Video
----------------

To extract video, call the `downloadVideo()` method of that specific
instance. For example, if our instance was defined "extractor", downloading
the video would be as easy as:

.. code-block:: java

  // path -> Direct path to Video File
  final Path path = extractor.downloadVideo();

The method returns a Path to the direct location of the video file.

.. warning::
  It is strongly recommended you run this method asynchronous! It may take a
  while depending on the video length and quality.

Extracting Audio
----------------

To extract audio, call the `extractAudio()` method of that specific
instance. Again, if our instance was defined "extractor", extraction
would be as simple as:

.. code-block:: java

  // path -> Direct path to Audio File
  final Path path = extractor.extractAudio();

The method returns a Path to the direct location of the audio file.

.. note::
  If the video file was not downloaded first, it will be automatically
  downloaded first during the process.

.. warning::
  It is strongly recommended you run this method asynchronous! It may take a
  while depending on the video length and attributes that you want to use for
  your audio file.

Important Warning
-----------------

.. warning::
  The methods `getVideo()` and `getAudio()` will return null if the video/audio
  has not been retrieved yet!

Method Events
-------------

You can override the methods `onVideoDownload()` and/or `onAudioExtraction()`
if you would like to display some message right before the video is being
downloaded and/or the audio is being extracted.

.. code-block:: java

  final YoutubeExtraction extractor = new YoutubeExtraction(
    "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
    "C://video",
    settings
  ) {
    @Override
    public void onVideoDownload() {
      System.out.println("The video is being downloaded!");
    }

    @Override
    public void onAudioExtraction() {
      System.out.println("The audio is being extracted!");
    }
  };
