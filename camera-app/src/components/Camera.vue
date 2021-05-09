<template>
   <div class="camera">
       <video autoplay class="feed" ></video>
       <button class="touchme" v-on:click="$emit('takePicture')"> <h4> Touch Me </h4></button>
   </div>
</template>

<script>
export default{
    name: "camera",
    methods : {
        init (){
            if ('mediaDevices' in navigator && 'getUserMedia' in navigator.mediaDevices){
                let constraints = {
                        video: {
                            width: {
                                min: 640,
                                ideal: 1280,
                                max: 1920
                            },
                            height : {
                                min: 360,
                                ideal: 720,
                                max: 1080

                            }
                        }
                    };
                navigator.mediaDevices.getUserMedia(constraints).then(stream => {
                    const videoPlayer = document.querySelector("video");
                    videoPlayer.srcObject = stream;
                    videoPlayer.play();
                });
            }
            else{
                alert("Cannot get media devices");
            }
        }
    },
    beforeMount(){
        this.init();
    }
    
 }
 </script>
 
<style>
.camera{
    width: 100vw;
    height: 100vh;
    padding: 25px;
    box-sizing: border-box;
    }

.feed{
      display: block;
      width: 100%;
      max-width: 1280px;

      margin: 0 auto;
      background-color: #171717;
      box-shadow: 4px 4px 12px 0px rgba(0, 0, 0, 0.25);
   }

 .touchme{

     display: block;
     width: 75px;
     height: 75px;
     border-radius: 50%;
     margin: 30px auto;

     background-color: red;
     border: 5px solid black;
     outline: none;

     cursor: pointer;

    }

</style>
