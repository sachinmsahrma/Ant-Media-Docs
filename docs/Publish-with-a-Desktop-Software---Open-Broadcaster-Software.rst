##############################
Publish With Desktop Softwares
##############################

OBS(Open Broadcaster Softeware) is Free and open source software for
video recording and live streaming. You can use either your PC’s
embedded camera or externally connected one as a video source with OBS.
Sound sources also can be configured with it. Ant Media Server is fully
compatible with OBS software.

Let’s have a look at step by step how to use OBS for streaming: 
Step 1 : Getting the OBS:
~~~~~~~~~~~~~~~~~~~~~~~~~

Download via its official `web page <https://obsproject.com/>`__. It has
Windows, Mac, and Linux releases.

Step 2 : Provide Sources:
~~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: https://ant-media.github.io/Ant-Media-Server/doc/images/obs_screenshot.jpg
   :alt: OBS (Open Broadcaster Software) interface

   OBS (Open Broadcaster Software) interface

By default, OBS starts to capture from your embedded camera if exists
after inilialized. You can add or remove video/audio source from Sources
section, such as an image can be broadcasted as a video source or
external microphone can be added as a audio source.

Step 3: Create RTMP URL for Ant Media Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  If your server configuration accepts any stream just use a RTMP URL
   like this “rtmp:///LiveApp/” Use IP address or server fqdn in the
   place of and use any id/name for the

-  If your server only accepts registered live streams, you need to
   create live stream by Management console or rest services.

   -  To reach the Management console go to http://:5080 address,
   -  Click one of the apps like “LiveApp” from Applications section and
      click “New Live Stream”.
   -  The server creates a live stream with an unique ID in the format
      of “rtmp:///LiveApp/325859929809451108600212”.
   -  You can copy this url with clicking “Publish URL” button.

.. figure:: https://ant-media.github.io/Ant-Media-Server/doc/images/management_console_new_live_stream.png
   :alt: Management Console New Live Stream

   Management Console New Live Stream

Step 4: Configure the OBS
~~~~~~~~~~~~~~~~~~~~~~~~~

You need to write live stream parameters to OBS in order to start
broadcasting. \* Click “Settings” then select “Stream” tab. \* Split the
rtmp:///LiveApp/ as the URL as the stream key \* Write URL and stream
key parameters as described in the below picture. Make sure that Stream
ID should be written to Stream Key field not to the URL.

.. figure:: https://ant-media.github.io/Ant-Media-Server/doc/images/OBS_Configuration.png
   :alt: OBS (Open Broadcaster Software) Stream Configuration

   OBS (Open Broadcaster Software) Stream Configuration

Step 5: Start Stream and Watch 🙂
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Close settings window and just click the “Start Streaming” button in
   the main window of OBS. You can watch stream from either Ant Media
   Management console or other platforms such as VLC player with same
   RTMP URL or with http:///LiveApp/streams/.m3u8 HLS
