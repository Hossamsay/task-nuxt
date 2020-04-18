<template>
       <no-ssr>
         <div>
           <nav class="navbar navbar-dark bg-dark">
                 <a class="navbar-brand" href="#">Home Page</a>
           </nav>
           <div class="embed-responsive embed-responsive-21by9">
                    <iframe id="player" type="text/html" 
                      src="https://www.youtube.com/embed/M7lc1UVf-VE?autoplay=1&controls=0&enablejsapi=1"
                      frameborder="0" style="border: solid 4px #37474F"></iframe>       
           </div>
           <iframe id="player" type="text/html" width="627" height="360"
                      src="https://www.youtube.com/embed/7K1sB05pE0A?autoplay=0&controls=1&enablejsapi=1"
                      frameborder="0" style="border: solid 4px #37474F"></iframe>
            <iframe id="player" type="text/html"  width="627" height="360"
                      src="https://www.youtube.com/embed/cBwNpKlhM8Q?autoplay=0&controls=0&enablejsapi=1"
                      frameborder="0" style="border: solid 4px #37474F"></iframe>
            <iframe id="player" type="text/html"  width="627" height="360"
                      src="https://www.youtube.com/embed/4m7msadL5iA?autoplay=0&controls=1&enablejsapi=1"
                      frameborder="0" style="border: solid 4px #37474F"></iframe>
            <iframe id="player" type="text/html"  width="627" height="360"
                      src="https://www.youtube.com/embed/80pRyn7fZRk?autoplay=0&controls=0&enablejsapi=1"
                      frameborder="0" style="border: solid 4px #37474F"></iframe>
         </div>
    </no-ssr>
</template>

<script>
  var tag = document.createElement('script');

      tag.src = "https://www.youtube.com/iframe_api";
      
      var firstScriptTag = document.getElementsByTagName('script')[0];
      firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
      var player;      
</script>
<script>
export default {
  methods: {
    onYouTubeIframeAPIReady() {
        player = new YT.Player('player', {
          events: {
            'onReady': onPlayerReady,
            'onStateChange': onPlayerStateChange,
            'onError': onPlayerError
            

          }
        })    
      },
      
       onPlayerReady(event) {
     event.target.setVolume(100);
    document.getElementById('player').style.borderColor = '#FF6D00';},

      changeBorderColor(playerStatus) {
    var color;
    if (playerStatus == -1) {
      color = "#37474F"; // unstarted = gray
    } else if (playerStatus == 0) {
      color = "#FFFF00"; // ended = yellow
    } else if (playerStatus == 1) {
      color = "#33691E"; // playing = green
    } else if (playerStatus == 2) {
      color = "#DD2C00"; // paused = red
    } else if (playerStatus == 3) {
      color = "#AA00FF"; // buffering = purple
    } else if (playerStatus == 5) {
      color = "#FF6DOO"; // video cued = orange
    }
    if (color) {
      document.getElementById('player').style.borderColor = color;
    }
  },
   onPlayerStateChange(event) {
     switch(event.data) {
          case 0:
            record('video ended');
            break;
          case 1:
            record('video playing from '+player.getCurrentTime());
            break;
          case 2:
            record('video paused at '+player.getCurrentTime());
        }
    changeBorderColor(event.data);
  },
  record(str){
        var p = document.createElement("p");
        p.appendChild(document.createTextNode(str));
        document.body.appendChild(p);
      },
       stopVideo() {
        player.stopVideo();
      },
     
  }
}

</script>
<style>

</style>
