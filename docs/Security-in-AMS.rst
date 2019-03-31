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

5- Hash Based Token in Streaming Sources

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

http://[IP_Address]/<Application_Name>/streams/streamID.mp4?token=tokenId

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

Please check this `blog <https://antmedia.io/secure-video-streaming/>`_ for more detailed information. 

4- CORS Filter in Streaming Sources
-------------------------------------
CORS(Cross-Origin Resource Sharing) Filter is active by default. 

If you remove CORS Filters in Applications(LiveApp or etc.), you should remove CORS Filters section in ServerFolder / webapps / Application(LiveApp or etc.) / WEB-INF / web.xml

.. figure:: https://antmedia.io/wp-content/uploads/2019/03/CORS-Filter-in-Application.png
   :alt: CORS Filter Setting in Applications
   
If you remove CORS Filters in root, you should remove CORS Filters section in ServerFolder / webapps / root / WEB-INF / web.xml
   
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/CORS-Filter-in-root.png
   :alt: CORS Filter Setting in root   
   
.. warning::
	If you remove CORS Filter, everyone can use your resources (m3u8, mp4 or etc) files and URL's
	
5- Hash Based Token in Streaming Sources
-----------------------------------------

.. tip::
	Hash Based Token feature is available for later versions of the 1.6.2+ version.
	
Firstly, the settings should be enabled from the settings file of the application.

.. code-block:: java

	settings.hashControlPublishEnabled=false
	settings.hashControlPlayEnabled=false
	tokenHashSecret=
	
Set true "settings.hashControlPublishEnabled" to enable secret based hash control for publishing operations, and "settings.hashControlPlayEnabled=" for playing operations.

.. tip::
	Also, do not forget to define a secret key for generating a hash value.
	
Publishing Scenario
^^^^^^^^^^^^^^^^^^^^^^^^^

Step 1. Generate a Hash
""""""""""""""""""""""""

You need to generate a hash value using the formula sha256(STREAM_ID + ROLE + SECRET) for your application and send to your clients. The values used for hash generation are:

.. code-block:: java

	STREAM_ID: The id of stream, generated in Ant Media Server.
	ROLE: It is either "play or "publish"
	SECRET: Shared secret key (should be defined in the setting file)
	
Step 2. Request with Hash
"""""""""""""""""""""""""""
The system controls hash validity during publishing or playing.

RTMP Publishing: You need to add a hash parameter to RTMP URL before publishing. Sample URL:

rtmp://[IP_Address]/<Application_Name>/<Stream_Id>?token=hash

WebRTC Publishing: Hash parameter should be inserted to publish WebSocket message.

{

    command : "publish",
	
    streamId : "stream1",
	
    token : "hash",
	
}

For details about WebRTC WebSocket messaging please visit `wiki page <https://github.com/ant-media/Ant-Media-Server/wiki/WebRTC-WebSocket-Messaging-Details>`_.

B) Playing Scenario
^^^^^^^^^^^^^^^^^^^^^^^^^

Step 1. Generate a Hash
"""""""""""""""""""""""""

You need to generate a hash value using the formula sha256(STREAM_ID + ROLE + SECRET) for your application and send to your clients. The values used for hash generation are:

.. code-block:: java

	STREAM_ID: The id of stream, generated in Ant Media Server.
	ROLE: It is either "play or "publish"
	SECRET: Shared secret key (should be defined in the setting file)

Step 2. Request with Hash
"""""""""""""""""""""""""""

Live Stream/VoD Playing: Same as publishing, the hash parameter is added to URL. Sample URL:

http://[IP_Address]/<Application_Name>/streams/<Stream_Id_or_Source_Name>?token=hash

WebRTC Playing: Again the hash parameter should be inserted to play WebSocket message.

{

    command : "play",

    streamId : "stream1",
	
    token : "hash",
	
}

Please have a look at the principles described in the wiki page.

Evaluation of the Hash
^^^^^^^^^^^^^^^^^^^^^^^^^

If related settings are enabled, Ant Media Server first generates hash values based on the formula sha256(STREAM_ID + ROLE + SECRET) using streamId, role parameters and secret string which is defined in the settings file. 

Then compare this generated hash value with clients hash value during authentication.

Once the hash is successfully validated by Ant Media Server, client is granted either to publish or play according to application setting and user request.