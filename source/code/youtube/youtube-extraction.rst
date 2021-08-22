Retrieving Video/Audio from Youtube Videos
==========================================

EzMediaCore provides an easy way to extract video and audio
from an existing Youtube link. This Youtube link can be either public or
unlisted.

Extracting Audio
----------------

To start off, we will be using the
`YoutubeVideoAudioExtractor <>`__
class. To instantiate one, we need three parameters: An instance of the library,
an `ExtractionSetting <https://github.com/MinecraftMediaLibrary/EzMediaCore/blob/master/main/src/main/java/io/github/pulsebeat02/ezmediacore/ffmpeg/YoutubeVideoAudioExtractor.java>`__,
a video link (must be Youtube), and finally a path to the audio file.

.. note::
  The Youtube link can be formatted in anyway such that the Youtube id is
  visible. In most cases, just copying the link (and it can be any format)
  will be fine. EzMediaCore is able to handle and extract the ids
  accordingly.

.. note::
  For more information about instantiating an AudioAttributes, take a look at:

  .. toctree::

    audio-attributes

As for an example of instantiating a new YoutubeVideoAudioExtractor, take a look at this
code snippet:

.. code-block:: java

  final AudioAttributes attributes = ...;
  final EzMediaCore core = ...;

  /*

  core -> The EzMediaCore instance
  attributes -> Audio Attributes
  "https://www.youtube.com/watch?v=dQw4w9WgXcQ" -> Youtube Link
  "C://video" -> Path to Directory

  */
  final YoutubeVideoAudioExtractor extractor = new YoutubeVideoAudioExtractor(
    core,
    attributes,
    "https://www.youtube.com/watch?v=dQw4w9WgXcQ",
    Path.of("C://extracted.ogg"),
  );

Then call any of the `execute()` methods to start the extraction.

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
