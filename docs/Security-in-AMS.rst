############################
Security in Ant Media Server
############################

Getting Started
---------------------------------------

This guide explains how to control Security on Ant Media Server. Briefly, our security procedures are; Token Control in Streaming Sources, IP Filter in REST API, CORS Filter in Streaming Sources, Hash Based Token.

1- IP Filter in REST API 

2- Accept Undefined Streams

3- Token Control in Streaming Sources 

4- CORS Filter in Streaming Sources.

5- Hash Based Token

1- IP Filter in REST API
--------------------------
.. tip::
	IP Filter feature is available for later versions of the 1.6.2+ version.

IP Filter feature usage is in Dashboard / Application(LiveApp or etc.) / Use IP Filtering for RESTful API section.

.. figure:: https://antmedia.io/wp-content/uploads/2019/03/RESTFUL-API-in-settings.png
   :alt: RESTFUL API Setting in AMS Dashboard

If you want some IP addresses to be able to access REST APIs, you should add IP's or IP Ranges in Dashboard / Application / Settings / Use IP Filtering for RESTful API

.. warning::
	If you delete 127.0.0.1, localhost web panel will no longer work. We have added 127.0.0.1 feature to people who have the same network. You can delete 127.0.0.1 if you do not want people with the same network to access REST APIs.

2- Accept Undefined Streams
-----------------------------
.. tip::
	Accept Undefined Streams feature is available for later versions of the 1.3.4+ version.
	
This setting shortly; Checking Live Stream is registered in Ant Media Server.

For example: If Stream Publishing enabled Allow All option, everyone can send Live Streaming(RTMP,WebRTC or etc) in Ant Media Server. If Stream Publishing enabled Allow Only In Database option, only registered streaming accept Ant Media Server. Registered mean, Dashboard/App/Live Streams/New Live Streams. 
 
You can find in more detail in here http://docs.antmedia.io/en/latest/Configurations.html#settings-file-under-applications settings.acceptOnlyStreamsInDataStore value

3- One Time Token Control in Streaming Sources
-----------------------------------------------
.. tip::
	Token Control feature is available for later versions of the 1.5.0+ version.
	
One Time Token Control feature usage is in Dashboard / Application(LiveApp or etc.) / Publish/Play with One-time Tokens section.
	
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/One-time-token-in-AMS.png
   :alt: One Time Token Setting in AMS Dashboard
	
By enabling this option, one time tokens are required for publishing and playing(WebRTC, RTRMP or etc). Publish/Play request without tokens will not be streamed.

If One-Time Token control option is active, then all publish and play requests should be sent with a token parameter.

RTMP URL usage:

rtmp://[IP_Address]/<Application_Name>/streamID?token=tokenId

Live Stream / VOD URL usage:

http://[IP_Address]/<Application_Name>/streams/250116815996644357614115.mp4?token=tokenId

Live Stream / VOD URL usage:

http://[IP_Address]/<Application_Name>/streams/250116815996644357614115.mp4?token=tokenId

WebRTC usage:

-Playing usage: Again the token parameter should be inserted to play WebSocket message. Also please have a look at the principles described in the `WebRTC playing wiki page <https://github.com/ant-media/Ant-Media-Server/wiki/WebRTC-WebSocket-Messaging-Details#playing-webrtc-stream>`_. 

WebSocket: ws://SERVER_NAME:5080/WebRTCAppEE/websocket

{
    command : "play",

    streamId : "stream1",

    token : "tokenId",

}

-Publishing usage: Again the token parameter should be inserted to play WebSocket message. Also please have a look at the principles described in the `WebRTC publishing wiki page <https://github.com/ant-media/Ant-Media-Server/wiki/WebRTC-WebSocket-Messaging-Details#publishing-webrtc-stream>`_.

WebSocket: ws://SERVER_NAME:5080/WebRTCAppEE/websocket

{

    command : "publish",
	
    streamId : "stream1",
	
    token : "tokenId",
	
}











