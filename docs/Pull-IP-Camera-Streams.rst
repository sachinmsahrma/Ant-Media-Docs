In addition to developing promising features in Ant Media Server, we
have added IP Camera support to it with the 1.3.0+ release. With this
feature,  users can pull IP Camera streams easily on management panel.
In other words, you don’t need to write any commands or use terminal.

The main critical point is that the IP Cameras should support ONVIF
standard. In fact, the majority of manufacturers already support this
standard because ONVIF make it easy to manage IP Cameras. All CRUD and
PTZ operations are based on well-defined SOAP messages.

Let’s have a look at how to pull stream from IP Camera. Of course,
first, you need to install Ant Media Server, please see documentation.

.. raw:: html

   <h2>

Add IP Camera

.. raw:: html

   </h2>

Select “LiveApp” from applications, then click “New Live Stream” and
select “IP Camera”. Fill camera name, camera username, and camera
password. You should define ONVIF URL of IP Camera. Generally, it is
IP-ADDRESS-OF-IPCAMERA:8080.  Another promising feature comes :) You can
use “auto-discovery” feature! If cameras and server are in the same
subnet, Ant Media Server automatically discovers them. The screenshot
of  auto-discovery result is shown below.

.. raw:: html

   <ol>

.. raw:: html

   </ol>

.. raw:: html

   <h2>

Watch IP Cameras

.. raw:: html

   </h2>

If the IP cameras are reachable and configured correctly, Ant Media
Server add theirs streams as live streams and starts to pull streams
from them. You can see its status on the management panel.

 

To watch the stream, just click the Play button on Actions.

Also, you can switch to Grid view if you have more than one camera and
want to see them simultaneously.

.. raw:: html

   <h2>

Record IP Camera Streams

.. raw:: html

   </h2>

The Ant Media Server can save IP Camera streams as MP4 format. In
addition, it record streams with defined periods such one hour, ten
hours interval . You can see these recorded files on VoD tab in the
management panel.

 

We hope you will be happy about this feature and the good news is that
it is offered in Community Edition. In other words, it is free! Please
keep in touch because we are releasing new versions, of course, new
features. If you have any questions or comments,  just send an email to
contact at antmedia dot io or fill the contact form.

 
