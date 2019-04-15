############################
Frequently Asked Questions
############################

How to reset Ant Media Server admin password?
-----------------------------------------------

**Step.1:**

Go to the installation directory of Ant Media Server.

.. code-block:: java

	cd /usr/local/antmedia

**Step-2:**

Remove "server.db" file.

.. code-block:: java

	sudo rm server.db

Step.3: Restart Ant Media Server.

.. code-block:: java

	sudo service antmedia restart

ICE failed, add a STUN server and see about:webrtc for more details
--------------------------------------------------------------------- 

if you get this error, you should check your UDP (5000-65535) Ports are open.

I enabled Object Detection, but doesn't work
-----------------------------------------------

You should add Adaptive Streaming in Application/Settings.

How to Reduce Latency in RTMP to HLS?
---------------------------------------

To reduce the HLS latency there are some parameters and it can be reduced to 8-10 secs for now.

- One of the parameter is having HLS segment time lower value which is by default 2 sec in Ant Media Server and you can decrease this value to have lower latency but then players start to poll server more frequently and it can be waste of resource usage.

- OBS Advanced Keyframe Interval: Second critical parameter is sending key frame in every 2 seconds(This value should consistent with HLS segment time) and it is critical to split videos into 2 sec duration segments. Open Broadcaster Software(OBS) sends key frame for every 10 seconds by default and the latency will increase to 30 seconds Key Frame Interval

.. figure:: https://i0.wp.com/antmedia.io/wp-content/uploads/2018/05/obs-keyframe-setting.png
   :alt:OBS Setting Page

After you have done these adjustments, your delay will be significantly reduced.

How to Enable SSL for Ant Media Server ?
-----------------------------------------

HTTPS and WSS(WebSocket Secure) is mandatory for Google Chrome to run WebRTC and WebSocket applications. In addition, developers want to serve their content with secure connection as well. The script in this document install Let's Encrypt SSL certificate.

Enabling SSL in Linux(Ubuntu)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Go to the folder where Ant-Media-Server is installed. Default directory is /usr/local/antmedia

.. code-block:: java

	cd /usr/local/antmedia
	
If there is a service that uses 80 port, you need to disable it. If your system has Apache Web Server, you need to disable it first such a command below

.. code-block:: java

	sudo service apache2 stop	
	
There should be a enable_ssl.sh file in the installation directory. Call the enable_ssl.sh with your domain name

.. code-block:: java

	sudo ./enable_ssl.sh example.com
	
v1.5+, enable_ssl.sh script supports external fullchain.pem and privkey.pem files. It's usage has been changed to

.. code-block:: java

	Usage:
	sudo ./enable_ssl.sh -d {DOMAIN_NAME}
	sudo ./enable_ssl.sh -f {FULL_CHAIN_FILE} -p {PRIVATE_KEY_FILE} -d {DOMAIN_NAME} 
	
If you disable any service that binds to 80 port such as Apache Web Server, enable it again

.. code-block:: java

	sudo service apache2 start
	
Make sure that your domain points to your server public IP address in the DNS records

If the above scripts returns successfully, SSL will be installed your server, you can use https through 5443. Like below

.. code-block:: java

	https://example.com:5443

.. warning::
	ATTENTION: If port 80 is used by some other process or it's forwarded to some other port, enable_ssl.sh will not be successful. Please disable the process or delete the port forwarding temporarily in running the enable_ssl.sh script above

How to Remove Port Forwarding?
--------------------------------

Check that which port forwardings exist in your system with below command.

.. code-block:: java

	sudo iptables -t nat --line-numbers -L
	
The command above should give an output live below

.. code-block:: java

	Chain PREROUTING (policy ACCEPT)
	num  target     prot opt source               destination         
	1    REDIRECT   tcp  --  anywhere             anywhere             tcp dpt:https redir ports 5443
	2    REDIRECT   tcp  --  anywhere             anywhere             tcp dpt:http redir ports 5080

	...
	
Delete the rule by line number. For instance to delete the http -> 5080 forwarding, run the command below

.. code-block:: java

	iptables -t nat -D PREROUTING 2

parameter 2 is the line number, if you want to delete https -> 5443, you should use 1 instead of 2

How to fix issue "Make sure that your domain name was entered correctly and the DNS A AAAA record(s)" ?
----------------------------------------------------------------------------------------------------------

- First of all make sure that A record is entered in your DNS settings and point to your server.

- If you are sure about that, check your ports whether 443 or 80 ports are not blocked or forwarded to any port.

- If you forward 80 or 443 ports to 5080 and 5443, then please remove these port forwarding settings as described in below "How to Remove Port Forwarding?".

How to fix “NotSupportedError” in publishing WebRTC stream in Ant Media Server ?
-----------------------------------------------------------------------------------

Problem is caused from attempting to access media source as discussed in https://stackoverflow.com/questions/34215937/getusermedia-not-supported-in-chrome.

To solve this problem you must enable SSL. You can follow instructions in this post https://antmedia.io/enable-ssl-on-ant-media-server.

WebRTC stream stops after a few seconds
-------------------------------------------

This issue is generally caused by unopened UDP ports. Please make sure that UDP ports 5000 to 65535 of your server are open.

In IOS, Chrome and Firefox cannot open the camera
---------------------------------------------------

This is an IOS bug: https://stackoverflow.com/questions/51501642/chrome-and-firefox-are-not-able-to-access-iphone-camera/53093348#53093348

Which codecs are supported by AntMedia?
-----------------------------------------

In video H264 is supported, In audio, for WebRTC, opus is supported and for HLS, AAC is supported.

Why are the WebRTC Bitrate limitations so low?
-----------------------------------------------

Let's remember the definition of WebRTC from its founders:

.. tip::
	"WebRTC is a free, open project that provides browsers and mobile applications with Real-Time Communications (RTC) capabilities via simple APIs. The WebRTC components have been optimized to best serve this purpose."

As you may know, the main purpose of WebRTC is Real-Time Communication.

Image quality is an opponent power against real-time (ultra-low latency) communication.

So, there should be a break-even point for the balance of latency and image quality.

The optimum video speed with the current processor and communication platforms is 2500 Kbps.

There are some references to this issue:

- A blog from WebRTC Expert Tashi Levent Levi:  https://bloggeek.me/webrtc-vs-zoom-video-quality/

- A paper from academia: http://wimnet.ee.columbia.edu/wp-content/uploads/2017/10/WebRTC-Performance.pdf

- Test results for the limits from webrtc-experiment.com 

.. code-block:: java
        
	https://www.webrtc-experiment.com/webrtcpedia/
    Maximum video bitrate on chrome is about 2Mb/s (i.e. 2000kbits/s).
    Minimum video bitrate on chrome is .05Mb/s (i.e. 50kbits/s).
    Starting video bitrate on chrome is .3Mb/s (i.e. 300kbits/s).

As a result, everyone needs to measure the best performant configuration of their infrastructure by changing them step-by-step.

Our suggestions are as follows:

.. code-block:: java

	- 20 for FPS is optimum; however, 10 and 15 should be examined.
	- 720p is good enough for video quality, especially for mobile platforms.
	- 1000 Kbps is optimum for 720p, 750 Kbps is also acceptable when FPS is 10.

Pixelating of frames in WebRTC
--------------------------------

This can cause a lot of things. If the broadcast values(Frame drop or etc) and server values (CPU or Ram etc.) are healthy, 3 things that matter to us can be listed below.

- Adaptive Streaming Setting. Here is default Setting in below.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: java

	Resolution   Video Bitrate (Kbps)  Audio Bitrate (Kbps)
	1080p              2000                       256
	720p               1500                       128 
	480p               1000                        75
	360p                800                        64
	240p                500                        32

These values change some different cases. Because everyone's scenario is different, these values are not fixed.

-WebRTC Framerate Setting
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Framerate is also a specific parameter. The framerate default parameter is 20. But as I said above, these values change your situation.

-Server Location
^^^^^^^^^^^^^^^^^^

It is more stable to broadcast physically near servers.

If broadcast quality problems occur, lower these values and select the server close to where you broadcast, I hope your quality problem will go away.

Frame Freezing in WebRTC Streaming
-------------------------------------

Frame Freezing problem is caused by frame Drop. The frame Drop reasons are listed below.

-Server Location
^^^^^^^^^^^^^^^^^^

It is more stable to broadcast physically near servers.

-Server Network Capacity
^^^^^^^^^^^^^^^^^^^^^^^^^^

For Media Streaming, servers with high network capacity are required. If your server's network capacity is low, you may experience frame drops. Also, Frame Drops causes Frame Freezing.


