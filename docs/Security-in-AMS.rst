############################
Security in Ant Media Server
############################

Getting Started
---------------------------------------

1- IP Filter in REST API 

2- Token Control in Streaming Sources.

3- CORS Filter in Streaming Sources.

4- Hash Based Token

This guide explains how to control Security on Ant Media Server. Briefly, our security procedures are; Token Control in Streaming Sources, IP Filter in REST API, CORS Filter in Streaming Sources, Hash Based Token.

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

2- Token Control in Streaming Sources