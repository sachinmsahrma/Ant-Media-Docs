Webhook Integration
===================

Ant Media Server provides webhooks for making your system/app know when
certain events occurs on the server. Therefore, you can register your
URL to Ant Media Server which makes POST request when a live stream is
started, finished or recorded. Firstly,  let’s look at how to register
your backend URL to Ant Media Server as a webhook. After that, we’ll
provide reference for webhooks.

.. raw:: html

   <h2>

Register Your Webhook URL

.. raw:: html

   </h2>

You can add default webhook URL to your streaming app on Ant Media
Server. In addition, it lets you add custom specific webhook URL’s in
creating broadcast.

.. raw:: html

   <h3>

Add default Webhook URL

.. raw:: html

   </h3>

In order to add default URL,  just follow the steps below

.. raw:: html

   <ul>

.. raw:: html

   <li>

Open your apps red5-web.properties  and add settings.listenerHookURL
property to that file. red5-web.properties file is under
webapps/<app_name>/WEB-INF  folder

.. raw:: html

   <pre>...
   settings.listenerHookURL=http://www.example.com/webhook/
   ...</pre>

.. raw:: html

   </li>

.. raw:: html

   <li>

Open your apps red5-web.xml file and add settings.listenerHookURL to the
app.settings bean.

.. raw:: html

   <pre class="p1"><span class="s1">...
   &lt;</span><span class="s2">bean</span><span class="s3"> </span><span class="s4">id</span><span class="s3">=</span>"app.settings"<span class="s3"> </span><span class="s4">class</span><span class="s3">=</span>"io.antmedia.AppSettings"<span class="s1">&gt;
   ...</span>
   <span class="s1">  &lt;</span><span class="s2">property</span><span class="s3"> </span><span class="s4">name</span><span class="s3">=</span>"listenerHookURL"<span class="s3"> </span><span class="s4">value</span><span class="s3">=</span>"${settings.listenerHookURL}"<span class="s3"> </span><span class="s1">/&gt;
   </span>...
   <span class="s1">&lt;/</span>bean&gt;
   ...</pre>

.. raw:: html

   </li>

.. raw:: html

   <li>

Restart the server on command line

.. raw:: html

   <pre>sudo service antmedia restart</pre>

.. raw:: html

   </li>

.. raw:: html

   </ul>

Right now, there is a default webhook URL for your app.

.. raw:: html

   <h3>

Add Custom Webhook for Streams

.. raw:: html

   </h3>

Ant Media Server provides creating streams through rest service.
Therefore, If you want to specify the webhook URL for each stream, you
can use createBroadcast method in rest service.  createBroadcast method
has Broadcast object parameter which has listenerHookURL field .

As a result,  you can set listenerHookURL for creating stream at Ant
Media Server.

Here is a sample JSON for using createBroadcast method with Postman

.. code:: json

   {
       "variables": [],
       "info": {
           "name": "samples",
           "_postman_id": "cbef37ab-d4ae-c349-4845-b4a91d1ab201",
           "description": "",
           "schema": "https://schema.getpostman.com/json/collection/v2.0.0/collection.json"
       },
       "item": [
           {
               "name": "http://localhost:5080/LiveApp/rest/broadcast/create",
               "request": {
                   "url": "http://localhost:5080/LiveApp/rest/broadcast/create",
                   "method": "POST",
                   "header": [
                       {
                           "key": "Content-Type",
                           "value": "application/json",
                           "description": ""
                       }
                   ],
                   "body": {
                       "mode": "raw",
                       "raw": "{\"name\":\"test_video\", \"listenerHookURL\":\"http://www.example.com/webhook\"}"
                   },
                   "description": "ListenerHookURL sample"
               },
               "response": []
           }
       ]
   }

Webhooks List
-------------

It’s time to know when Ant Media Server calls webhooks with which
parameters. Here is a simple list for that

-  liveStreamStarted: Ant Media server calls this hook when a new live
   stream is started. It sends **POST
   (application/x-www-form-urlencoded)** request to URL with following
   variables

   -  id:  stream id of the broadcast
   -  action: “liveStreamStarted”
   -  streamName: stream name of the broadcast. It can be null.
   -  category:  stream category of the broadcast. It can be null.

-  liveStreamEnded: Ant Media Server calls this hook when a live stream
   is ended. It sends **POST(application/x-www-form-urlencoded)**
   request to URL with following variables.

   -  id: stream id of the broadcast
   -  action: “liveStreamEnded”
   -  streamName: stream name of the broadcast. It can be null.
   -  category: stream category of the broadcast. It can be null.

-  vodReady: Ant Media Server calls this hook when the recording of the
   live stream is ended. It sends
   **POST(application/x-www-form-urlencoded)** request to URL with
   following variables.

   -  id: stream id of the broadcast
   -  action: “vodReady”
   -  vodName:  vod file name
   -  vodId:  vod id in the datastore

That’s all. As a result, you can take some custom actions according to
your project by checking action variable in your backend URL.

We hope this post will help you to make automation in your project. 
Please keep in touch if you have any question. We will be happy if we
can help you.

   **Attention:** Please process the result in your backend URL as soon
   as possible because these callbacks is called in event loop threads
   that does not support long running operations.

 
