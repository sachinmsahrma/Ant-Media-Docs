Ant Media Server 1.2.0+ Enterprise Edition supports adaptive low latency
WebRTC streaming.

In addition, Ant Media Server can \* Record WebRTC streams as MP4 and
MKV \* Convert WebRTC streams to adaptive live HLS \* Create previews in
PNG format from WebRTC streams

Download
--------

Firstly, you need to have Ant Media Server Enterprise Edition. If you
are a personal user and just want to try, contact with us at
`antmedia.io <https://antmedia.io>`__. We will reply back by providing
Ant Media Server Enterprise Edition to try.

If you are a professional user and need support, you can buy support at
`antmedia.io <https://antmedia.io>`__ as well

Quick Start
-----------

*Ant Media Server 1.2.0+ runs on Linux and Mac not on Windows.*

Let’s start, we assume that you have got Enterprise Edition somehow and
downloaded to your local computer

1. Follow the instructions on [Getting Started] for installation
   (https://github.com/ant-media/Ant-Media-Server/wiki/Getting-Started)

2. Open the browser(Chrome or Firefox) and go to the
   ``http://localhost:5080/WebRTCAppEE``. Let browser access your camera
   and mic unless it cannot send WebRTC Stream to the server

   .. figure:: https://ant-media.github.io/Ant-Media-Server/doc/images/1_Open_WebRTCAppEE_and_Let_Browser_Access_Cam_and_Mic.jpg
      :alt: Open WebRTCAppEE

      Open WebRTCAppEE

   *WebRTCAppEE stands for WebRTCApp Enterprise Edition*

3. Write stream name or leave it as default and Press
   ``Start Publishing`` button. After you press the button, “Publishing”
   blinking text should appear

   .. figure:: https://ant-media.github.io/Ant-Media-Server/doc/images/2_Press_Publish_Button.jpg
      :alt: Press Start Publishing button

      Press Start Publishing button

4. Go to the ``http://localhost:5080/WebRTCAppEE/player.html``

   .. figure:: https://ant-media.github.io/Ant-Media-Server/doc/images/3_Go_to_Play_Page.jpg
      :alt: Go to the player.html

      Go to the player.html

5. Press ``Start Play`` button. After you press the button, webrtc
   stream should be started

   .. figure:: https://ant-media.github.io/Ant-Media-Server/doc/images/4_Press_Start_Play_Button.jpg
      :alt: Press Start Playing Button

      Press Start Playing Button

6. Open ``http://localhost:5080/WebRTCAppEE/player.html`` in other tabs
   and Press ``Start Playing`` button again to check how it plays and
   what the latency is.

Running on Remote Instances - Enable SSL For Ant Media Server Enterprise
------------------------------------------------------------------------

If you are running the Ant Media Server Enterprise Edition in remote
computer/instances, you may need SSL. If so, please follow the Enable
SSL doc or `this blog
post <https://antmedia.io/enable-ssl-on-ant-media-server/>`__.

Feedbacks
---------

Please let us know your feedbacks about the latency and streaming or any
other issue you have faced so that we can improve and let you try and
use.

You can use contact form at `antmedia.io <https://antmedia.io>`__ or
``contact at antmedia dot io`` e-mail to send your feedbacks

Thank you

`Ant Media <https://antmedia.io>`__
