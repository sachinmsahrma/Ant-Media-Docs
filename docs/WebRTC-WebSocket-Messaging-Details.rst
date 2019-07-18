This documentation is for developers who needs to implement signalling
between Ant Media Server and clients for publishing & playing streams.
Let’s make it step by step

Publishing WebRTC Stream
~~~~~~~~~~~~~~~~~~~~~~~~

1. Client connects to Ant Media Server through WebSocket. URL of the
   WebSocket interface is something like

::

   ws://SERVER_NAME:5080//WebRTCApp/websocket

2. Client sends publish JSON command to the server with stream name
   parameter. (Remove token parameter if token control is not enabled)

.. code:: json

   {
       command : "publish",
       streamId : "stream1",
       token : "tokenId",
   }

3. If Server accepts the stream, it replies back with start command

.. code:: json

   {
       command : "start",
       streamId : "stream1",
   }

4. Client inits peer connections, creates offer sdp and send the sdp
   configuration to the server with takeConfiguration command

.. code:: json

   {
      command : "takeConfiguration",
      streamId : "stream1",
      type : "offer",  
      sdp : "${SDP_PARAMETER}"
   }

5. Server creates answer sdp and send the sdp configuration to the
   client with takeConfiguration command

.. code:: json

   {
      command : "takeConfiguration",
      streamId : "stream1",
      type : "answer",  
      sdp : "${SDP_PARAMETER}"
   }

6. Client and Server get ice candidates several times and sends to each
   other with takeCandidate command

.. code:: json

   {
       command : "takeCandidate",
       streamId : "stream1",
       label : "${CANDIDATE.SDP_MLINE_INDEX}",
       id : "${CANDIDATE.SDP_MID}",
       candidate : "${CANDIDATE.CANDIDATE}"
   }

7. Clients sends stop JSON command to stop publishing

.. code:: json

   {
       command : "stop",
       streamId: "stream1"
   }

Playing WebRTC Stream
~~~~~~~~~~~~~~~~~~~~~

1. Client connects to Ant Media Server through WebSocket.

::

   ws://SERVER_NAME:5080/WebRTCAppEE/websocket

2. Client sends play JSON command to the server with stream name
   parameter. (Remove token parameter if token control is not enabled)

.. code:: json

   {
       command : "play",
       streamId : "stream1",
       token : "tokenId",

   }

3. If Server accepts the stream, it replies back with offer command

.. code:: json

   {
      command : "takeConfiguration",
      streamId : "stream1",
      type : "offer",  
      sdp : "${SDP_PARAMETER}"
   }

5. Client creates answer sdp and send the sdp configuration to the
   server with takeConfiguration command

.. code:: json

   {
      command : "takeConfiguration",
      streamId : "stream1",
      type : "answer",  
      sdp : "${SDP_PARAMETER}"
   }

6. Client and Server get ice candidates several times and sends to each
   other with takeCandidate command

.. code:: json

   {
       command : "takeCandidate",
       streamId : "stream1",
       label : "${CANDIDATE.SDP_MLINE_INDEX}",
       id : "${CANDIDATE.SDP_MID}",
       candidate : "${CANDIDATE.CANDIDATE}"
   }

7. Clients sends stop JSON command to stop playing

.. code:: json

   {
       command : "stop",
       streamId: "stream1",
   }

Peer to Peer WebRTC Stream
~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Peers connects to Ant Media Server through WebSocket.

::

   ws://SERVER_NAME:5080/WebRTCAppEE/websocket

2. Client sends join JSON command to the server with stream name
   parameter.

.. code:: json

   {
       command : "join",
       streamId : "stream1",
   }

If there is only one peer in the stream1, server waits for the other
peer to join the room.

3. When second peer joins the stream, server sends start JSON command to
   the first peer

.. code:: json

   {
       command : "start",
       streamId : "stream1",
   }

4. First peer create offer sdp and send to the server with
   takeConfiguration command,

.. code:: json

   {
      command : "takeConfiguration",
      streamId : "stream1",
      type : "offer",  
      sdp : "${SDP_PARAMETER}"
   }

Server relays the offer sdp to the second peer

5. Second peer creates answer sdp and sends to the server with
   takeConfiguration command

.. code:: json

   {
      command : "takeConfiguration",
      streamId : "stream1",
      type : "answer",  
      sdp : "${SDP_PARAMETER}"
   }

Server relays the answer sdp to the first peer

6. Each peers get ice candidates several times and sends to each other
   with takeCandidate command through server

.. code:: json

   {
       command : "takeCandidate",
       streamId : "stream1",
       label : "${CANDIDATE.SDP_MLINE_INDEX}",
       id : "${CANDIDATE.SDP_MID}",
       candidate : "${CANDIDATE.CANDIDATE}"
   }

7. Clients sends leave JSON command to leave the room

.. code:: json

   {
       command : "leave",
       streamId: "stream1"
   }

Conference WebRTC Stream
~~~~~~~~~~~~~~~~~~~~~~~~

1. Peers connects to Ant Media Server through WebSocket.

::

   ws://SERVER_NAME:5080/WebRTCAppEE/websocket

2. Client sends join JSON command to the server with room name
   parameter.

.. code:: json

   {
       command : "joinRoom",
       room : "room1",
   }

3. Server notifies the client with available streams in the room

.. code:: json

   {
       command : "notification",
       definition : "joinedTheRoom",
       streamId: "unique_stream_id_returned_by_the_server"
       streams: [
           "stream1_in_the_room",
           "stream2_in_the_room",
           .
           .
           .
       ]
   }

``streamId`` returned by the server is the stream id client uses to
publish stream to the room. ``streams`` is the json array which client
can play via WebRTC. Client can play each stream by play method above.
This strams array can be empty if there is no stream in the room.

4. When there is a new guy joined the room, server sends below message
   to each peer in the room.

.. code:: json

   {
       command : "notification",
       definition : "streamJoined",
       streamId: "new_stream_id_joined_the_room"
       
   }

Client can play the new joined stream with the streamId by the play
method above.

5. When someone leaves the room, server sends the below message to each
   peer in the room.

.. code:: json

   {
       command : "notification",
       definition : "streamLeaved",
       streamId: "stream_id_leaved_the_room"
   }

Client can update/remove the related video views from UI.

6. Any user can leave the room by sending below message

.. code:: json

   {
       command : "leaveFromRoom",
       room: "roomName"
   }

WebSocket Error Callbacks
~~~~~~~~~~~~~~~~~~~~~~~~~

-  ``noStreamNameSpecified``: it is sent when stream id is not specified
   in the message.

.. code:: json

   {
       command : "error",
       definition : "noStreamNameSpecified",
   }

-  ``not_allowed_unregistered_streams``: This is sent back to the user
   if the publisher wants to send a stream with an unregistered id and
   server is configured not to allow this kind of streams

.. code:: json

   {
       command : "error",
       definition: "not_allowed_unregistered_streams",
   }

-  ``no_room_specified``: This is sent back to the user when there is no
   room specified in joining the video conference.

.. code:: json

   {
       command : "error",
       definition : "no_room_specified",
   }

-  ``unauthorized_access``:This is sent back to the user when the token
   is not validated

.. code:: json

   {
       command : "error",
       definition : "unauthorized_access",
   }

-  ``no_encoder_settings``:This is sent back to the user when there are
   no encoder settings available in publishing the stream.

.. code:: json

   {
       command : "error",
       definition : "no_encoder_settings",
   }

-  ``no_peer_associated_before``: This is peer to peer connection error
   definition.It is sent back to the user when there is no peer
   associated with the stream.

.. code:: json

   {
       command : "error",
       definition : "no_peer_associated_before",
   }

-  ``notSetLocalDescription``: It is send when local description is not
   set successfully

.. code:: json

   {
       command : "error",
       definition : "notSetLocalDescription",
   }
