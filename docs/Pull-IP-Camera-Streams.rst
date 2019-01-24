In addition to developing promising features in Ant Media Server, we
have added IP Camera support to it with the 1.3.0+ release. With this
feature,  users can pull IP Camera streams easily on management panel.
In other words, you don’t need to write any commands or use terminal.

The main critical point is that the IP Cameras should support ONVIF
standard. In fact, the majority of manufacturers already support this
standard because ONVIF make it easy to manage IP Cameras. All CRUD and
PTZ operations are based on well-defined SOAP messages.

.. figure:: https://antmedia.io/wp-content/uploads/2018/03/cctv-onvif-560.jpg
   :alt: onvif


Let’s have a look at how to pull stream from IP Camera. Of course,
first, you need to install Ant Media Server, please see documentation.

Add IP Camera
-------------

Select “LiveApp” from applications, then click “New Live Stream” and
select “IP Camera”. Fill camera name, camera username, and camera
password. You should define ONVIF URL of IP Camera. Generally, it is
IP-ADDRESS-OF-IPCAMERA:8080.  Another promising feature comes :) You can
use “auto-discovery” feature! If cameras and server are in the same
subnet, Ant Media Server automatically discovers them. The screenshot
of  auto-discovery result is shown below.

Watch IP Cameras
----------------

If the IP cameras are reachable and configured correctly, Ant Media
Server add theirs streams as live streams and starts to pull streams
from them. You can see its status on the management panel.

To watch the stream, just click the Play button on Actions.

.. figure:: https://antmedia.io/wp-content/uploads/2018/03/Screenshot-from-2018-03-21-21-15-15-1024x502.png
   :alt: ONVIF IP Camera watching

Also, you can switch to Grid view if you have more than one camera and
want to see them simultaneously.

.. figure:: https://antmedia.io/wp-content/uploads/2018/03/Screenshot-from-2018-03-21-21-17-47-1024x494.png
   :alt: 

Record IP Camera Streams
------------------------

The Ant Media Server can save IP Camera streams as MP4 format. In
addition, it record streams with defined periods such one hour, ten
hours interval . You can see these recorded files on VoD tab in the
management panel.

.. figure:: https://antmedia.io/wp-content/uploads/2018/03/Screenshot-from-2018-03-21-21-19-46-1024x347.png
   :alt: 

We hope you will be happy about this feature and the good news is that
it is offered in Community Edition. In other words, it is free! Please
keep in touch because we are releasing new versions, of course, new
features. If you have any questions or comments,  just send an email to
contact at antmedia dot io or fill the contact form.

 
