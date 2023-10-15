<template>
    <div class="container">
        
            <div class="box" v-for="(addr, index) in addrs">
                <span></span>
                <span></span>
                <span></span>
                <span></span>
                <video class="MyVideo" :id="video(index)"> </video>
            </div>
        
    </div>
</template>


<script>
    //import WebRTCStreamerElement from "../../api/webrtc/webrtc-streamer-element.js";
    //import Video2 from "./Video2.vue";
    import WebRtcStreamer from "../../api/webrtc/webrtcstreamer.js";
    export default {
        data() {
            var webRtcServerList = []
            return {
                webRtcServerList : webRtcServerList,
                msg: 'ok',
                addrs : [
                    "rtsp://admin:link123456@192.168.10.232:554/stream1",
                    "rtsp://admin:link123456@192.168.10.232:554/stream2"
                ]
            }
        },
        methods : {
            video(index){
		        return "video"+index;
            }
        },
        mounted(){
            var webRtcServer = null;
            for(var i = 0; i < this.addrs.length; i++){
                webRtcServer = new WebRtcStreamer(this.video(i),"http://" + "localhost" + ":8000");
                webRtcServer.connect(this.addrs[i]);
                this.webRtcServerList.push(webRtcServer);
            }
        },
        beforeUnmount(){
            for(webRtcServer in this.webRtcServerList){
                webRtcServer.disconnect();
            }
        }
    }
</script>

<style scoped>
  .MyVideo {
    width: 400px;
    height: auto;
  }

  *{
  margin:0;
  padding:0;
}

.container{  
  height: 100%;
  width: 100%;
  margin-left: 180px;
  margin-top: 180px;
  
}
body{
  background-color: #111845;
}

.background-img{
  background-image: url("https://3.bp.blogspot.com/-piZWCW2uUbg/W2fPXxkWZgI/AAAAAAAAOu0/eydmMjTIqcwLMHEEr2H7imqoRTxMw4o9QCLcBGAs/s1600/among_trees_night_dribbble.png");
height: 400px;
  width: 800px;

  position: relative;
}

.box{
  transform: translate(-50%, -50%);
  width: 400px;
  height: 400px;

  background: #111845a6;
  box-sizing: border-box;
  overflow: hidden;
  box-shadow: 0 20px 50px rgb(22, 22, 22);
  border: 2px solid #2a3cad;
  color: white;
  margin: 50px;
}

.box:before{
  content: '';
  position:absolute;
  top:0;
  left:-100%;
  width:100%;
  height:100%;
  background: rgba(255,255,255,0.1);
  transition:0.5s;
  pointer-events: none;
}

.box:hover:before{
  left:-50%;
  transform: skewX(-5deg);
}


.box .content{
  position:absolute;
  top:15px;
  left:15px;
  right:15px;
  bottom:15px;
  border:1px solid #f0a591;
  padding:20px;
  text-align:center;
  box-shadow: 0 5px 10px rgba(9,0,0,0.5);
  
}

.box span{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: block;
  box-sizing: border-box;
  
}

.box span:nth-child(1)
{
  transform:rotate(0deg);
}

.box span:nth-child(2)
{
  transform:rotate(90deg);
}

.box span:nth-child(3)
{
  transform:rotate(180deg);
}

.box span:nth-child(4)
{
  transform:rotate(270deg);
}

.box span:before
{
  content: '';
  position: absolute;
  width:100%;
  height: 2px;
  background: #50dfdb;
  animation: animate 4s linear infinite;
}

@keyframes animate {
  0% {
  transform:scaleX(0);
  transform-origin: left;
  }
  50%
  {
    transform:scaleX(1);
  transform-origin: left;
  }
  50.1%
  {
    transform:scaleX(1);
  transform-origin: right;
    
  }
  
  100%
  {
    transform:scaleX(0);
  transform-origin: right;
    
  }
}


</style>