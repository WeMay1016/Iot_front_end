<template>
    <div id="monitorHead">
      <!-- <webrtc-streamer url="rtsp://wowzaec2demo.streamlock.net/vod/mp4:BigBuckBunny_115k.mov"></webrtc-streamer> -->
      <video id="video1" class = 'video'></video>
      <video id="video2" class = 'video'></video>
    </div>
</template>


<script>
  //import WebRTCStreamerElement from "../../api/webrtc/webrtc-streamer-element.js";
  import WebRtcStreamer from "../../api/webrtc/webrtcstreamer.js";
  export default {
    data() {
      return {
        msg: '',
        //web: webRtcServer,
        sendMsg:'111' // 默认为可以查看所有传感器节点（1:可视; 0:不可视）
      }
    },
    components: {
    },
    methods:{
    },
    amount:{
    },
    beforeCreate(){
    },
    mounted(){
      var webRtcServer = null;
      webRtcServer = new WebRtcStreamer("video1","http://" + "localhost" + ":8000");
	    webRtcServer.connect("rtsp://admin:link123456@192.168.10.232:554/stream1");

      webRtcServer = new WebRtcStreamer("video2","http://" + "localhost" + ":8000");
	    webRtcServer.connect("rtsp://admin:link123456@192.168.10.232:554/stream2");
    },
    beforeUnmount(){
        //webRtcServer.close();
    }
  }
</script>

<style scoped>

  .video {
    height: 30%;
    width: 30%;
  }

  #monitorHead{

  }
</style>
