Inside of The Box
=================

What is in Docker Container?
----------------------------

After building the dockerfile we get a docker image which contains all necessary software and artifacts for load test. 

Installed Softwares
~~~~~~~~~~~~~~~~~~~
- **Java:** Used by WebRTCTest Tool and test web application.
- **FFmpeg:** Used for RTMP publishing and, RTMP and HLS playing. 
- **Ant Media Tools:** 
  -  WebRTCTest (used for both publishing and playing with WebRTC). 
  -  Test web application (used for managing tests). 

Directory Structure
~~~~~~~~~~~~~~~~~~~

::

   /home/antmedia/test
   |-- webrtctest
   |   |-- run.sh
   |   |-- lib
   |   '-- webrtctest.jar
   |
   |-- loadtester.jar
   |
   |-- Test.mp4
   |
   '-- results      (created after first test)
       '-- YYYY-MM-DD_hh:mm:ss
