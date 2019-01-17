Seamless switch between WebRTC Screen Sharing & Camera is available on
both Community and Enterprise Edition. We mean by seamless is that you
can switch between Screen & Camera in the same session.

.. raw:: html

   <h2>

Try WebRTC Screen Sharing

.. raw:: html

   </h2>

Firstly, just let me tell how to try it. After that I will give some
information about JavaScript API and chrome extension.

.. raw:: html

   <ol>

.. raw:: html

   <li>

 Install Ant Media Server to your server in the cloud with Getting
Started. In order to download community edition, visit main page or if
you want to try Enterprise edition, keep in touch.

.. raw:: html

   </li>

.. raw:: html

   <li>

 Go to WebRTC publishing web page which is https://FQDN:5443/WebRTCApp
(Community E. ) or https://FQDN:5443/WebRTCAppEE (Enterprise E.). By the
way,  you need to assign a domain to your server and install
SSL. Otherwise, chrome does not let you access the camera or screen.

.. raw:: html

   <ul>

.. raw:: html

   </ul>

.. raw:: html

   </li>

.. raw:: html

   <li>

Install Chrome Extension by clicking on the link or directly from Chrome
WebStore. Luckily, source code of the extension is also available on
github.

.. raw:: html

   </li>

.. raw:: html

   <li>

 Return back to WebRTC Publish page and click Screen Share Checkbox

.. raw:: html

   </li>

.. raw:: html

   <li>

Screen is going to be shared on the video element

.. raw:: html

   </li>

.. raw:: html

   <li>

Click “Start Publishing” and also check/uncheck “Screen Share” box while
publishing in the same session. MP4 file or HLS stream will record the
screen or your camera according to your preference. You can watch the
stream live on web panel via HLS.

.. raw:: html

   </li>

.. raw:: html

   </ol>

.. raw:: html

   <h2>

Implementing WebRTC Screen Sharing

.. raw:: html

   </h2>

We just add some simple functions to js/webrtc_adaptor.js file to
seamless switch between screen sharing and camera. You can take a look
at the source code of WebRTCApp/index.html  to see the full
implementation. Meanwhile, let me give some highlights about JavaScript
API.

.. raw:: html

   <ul>

.. raw:: html

   <li>

Firstly, There is a new callback with
“screen_share_extension_available”. If callback function is called with
this parameter, it means that Ant Media Server Screen Share extension is
ready to use in the Chrome.

.. raw:: html

   </li>

.. raw:: html

   </ul>

.. code:: javascript


       var webRTCAdaptor = new WebRTCAdaptor({
       websocket_url : websocketURL,
       mediaConstraints : mediaConstraints,
       peerconnection_config : pc_config,
       sdp_constraints : sdpConstraints,
       localVideoId : "localVideo",
       debug:true,
       callback : function(info, description) {
            if (info == "initialized") {
           console.log("initialized");
                   
            } else if (info == "publish_started") {
           //stream is being published
           console.log("publish started");     
            } else if (info == "publish_finished") {
           //stream is being finished
           console.log("publish finished");        
            }
            else if (info == "screen_share_extension_available") {
           console.log("screen share extension available");    
             }
             else if (info == "closed") {
             //console.log("Connection closed");
             if (typeof description != "undefined") {
               console.log("Connecton closed: " + JSON.stringify(description));
             }
             }
       },
       callbackError : function(error, message) {
           //some of the possible errors, NotFoundError, SecurityError,PermissionDeniedError
               
               console.log("error callback: " +  JSON.stringify(error));
       }
   });

.. raw:: html

   <ul>

.. raw:: html

   <li>

Secondly, if extension is available in the Chrome, you only need to call
“webRTCAdaptor.switchDesktopCapture(streamId);” function to switch the
Screen Sharing

.. raw:: html

   <blockquote>

webRTCAdaptor.switchDesktopCapture(streamId);

.. raw:: html

   </blockquote>

.. raw:: html

   </li>

.. raw:: html

   <li>

Lastly, to switch back to camera,  just again call to
“webRTCAdaptor.switchVideoCapture(streamId);” function.

.. raw:: html

   <blockquote>

webRTCAdaptor.switchVideoCapture(streamId);

.. raw:: html

   </blockquote>

.. raw:: html

   </li>

.. raw:: html

   </ul>

Finally, that’s all. I hope this blog post will help some guys. You can
use this feature on your project.

If you have any question, please keep in touch.
