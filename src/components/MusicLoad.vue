<template>
<button @click="showSong" class="action-btn menu"><i class="fas fa-music fa-lg"></i><i class="fas fa-bars fa-lg"></i></button>

<div class="nav">
    <ul>
        <li @click="playList(0)">AG_BABY- Adekunle Gold ft BlackMan</li>
        <li @click="playList(1)">Dami_Duro- Davido</li>
        <li @click="playList(2)">Holy- Justin Bieber ft Chance</li>
        <li @click="playList(3)">I'm_The_One- DJ Khaled</li>
        <li @click="playList(4)">Jowo- Davido</li>
        <li @click="playList(5)">Own_It- Stormzy ft BurnaBoy</li>
        <li @click="playList(6)">Shele_gan_gan- Lil Kesh</li>
        <li @click="playList(7)">Someone_You_Loved- Lewis Capaldi</li>
        <li @click="playList(8)">Stay_High- Juice WRLD</li>
    </ul>
</div>
<div class="title">
    <h1><span>Vue</span>Music<span><button class="action-btn"><i class="fas fa-music fa-2x"></i></button></span></h1>
     <p>Music for the soul...</p>
</div>

<div class="music-container">
    <div>
        <img :src="cover" alt="" class="cover">
    </div>
    <div class="showcase">
        <p class="music-title">{{title}}</p>
        <p class="music-singer">{{artist}}</p>
    </div>
    <div @click="setProgress" class="progress-container">
        <div class="progress">
        </div>
    </div>
    <audio @timeupdate="updateProgress" @ended="nextSong" :src="song" id="audio" type="audio/mp3"></audio>
    <div class="controls">
        <button @click="prevSong" class="action-btn"><i class="fas fa-backward"></i></button>
        <button id="play" @click="playToggle" class="action-btn action"><i class="fas fa-play"></i></button>
        <button @click="nextSong" class="action-btn"><i class="fas fa-forward"></i></button>
    </div>

</div>
</template>

<script>
export default {
    data(){
        return{
            Music:[
                {
                title:"AG-BABY",
                song:require("../assets/music/AG-BABY.mp3"),
                artist:"Adekunle Gold ft BlackMan",
                cover:require("../assets/img/AG-BABY.jpg")
                },
                 {
                title:"Dami Duro",
                song:require("../assets/music/Dami-Duro.mp3"),
                artist:"Davido",
                cover:require("../assets/img/dami-duro.jpg")
                },
                 {
                title:"Holy",
                song:require("../assets/music/Holy.mp3"),
                artist:"Justin Beiber ft Chance",
                cover:require("../assets/img/holy.jpg")
                },
                 {
                title:"I'm the One",
                song:require("../assets/music/I'm-the-one.mp3"),
                artist:"DJ Khaled",
                cover:require("../assets/img/am-the-one.jpg")
                },
                 {
                title:"Jowo",
                song:require("../assets/music/Jowo.mp3"),
                artist:"Davido",
                cover:require("../assets/img/jowo.jpg")
                },
                 {
                title:"Own It",
                song:require("../assets/music/Own-It.mp3"),
                artist:"Stormzy ft BurnaBoy",
                cover:require("../assets/img/own-it.jpg")
                },
                 {
                title:"Shele gan gan",
                song:require("../assets/music/Shele-gan-gan.mp3"),
                artist:"Lil Kesh",
                cover:require("../assets/img/shele.jpg")
                },
                 {
                title:"Someone You Loved",
                song:require("../assets/music/Someone_You_Loved.mp3"),
                artist:"Lewis Capaldi",
                cover:require("../assets/img/someone.jpg")
                },
                 {
                title:"Stay High",
                song:require("../assets/music/Stay_High.mp3"),
                artist:"Juice WRLD",
                cover:require("../assets/img/stay-high.jpeg")
                },
                ],

                play:false,
                show:false,
                title: '',
                song:'',
                artist:'',
                cover:'',
                index:0,
        }
    },
    methods:{
        start(){
          const musicList = this.Music;
           let currentSong = this.index;

           this.loadSong(musicList[currentSong])
        },
       playToggle(){
          this.play=!this.play
          const container = document.querySelector('.music-container')
           if(this.play == true){
               container.classList.add('play')
               this.playSong()
           }else{
              container.classList.remove('play')
               this.pauseSong()
           }
       },
       playSong(){
            const container = document.querySelector('.music-container')
            container.classList.add('play')
            const audio = document.getElementById('audio');
            audio.play()
            audio.autoplay=true;
            const play= document.querySelector('#play')
            play.querySelector('i.fas').classList.remove('fa-play')
            play.querySelector('i.fas').classList.add('fa-pause')
       },
       pauseSong(){
            const audio = document.getElementById('audio');
            audio.pause()
            const play= document.querySelector('#play')
            play.querySelector('i.fas').classList.add('fa-play')
            play.querySelector('i.fas').classList.remove('fa-pause')
            
       },
       loadSong(song){
           this.title=song.title;
           this.song=song.song;
           this.artist=song.artist;
           this.cover=song.cover;
       },
       playList(num){
           this.index=num;
           this.start()
           this.playSong()
            const nav = document.querySelector('.nav')
            setTimeout(()=> {
                nav.style.opacity=0;

            },1000)

       },
       nextSong(){
           this.index++
           const music = this.Music

           if(this.index === music.length){
              this.index = 0
           }
           this.start()
           this.playSong()

       },
       prevSong(){
        this.index--
        const music = this.Music
          if(this.index < 0){
              this.index = music.length-1
           }
        this.start()
       },
       updateProgress(e){
           const progress = document.querySelector('.progress')
           const{duration, currentTime}= e.srcElement
           const progressPercent = (currentTime/duration) * 100

          progress.style.width = `${progressPercent}%`
       },
       setProgress(e){
            const audio = document.getElementById('audio');
           const width = 300
          const clickX = e.offsetX;
           const duration= audio.duration;

          audio.currentTime = (clickX/width)*duration
       },
       showSong(){
           const nav = document.querySelector('.nav')
           this.show=!this.show;
           if(this.show){
             nav.style.opacity=0;
           }
           else{
               nav.style.opacity=1
           }
       }
    
    },
    mounted(){
           this.start()
    }
    

}
</script>

<style>
*{
    box-sizing: border-box;
    margin:0;
}
body{
    height: 80vh;
    display: flex;
    justify-content: center;
    align-items: center;
    position:relative;

}
.title{
    color:white;
}
.title h1{
        font-size:40px;
        font-weight: bold;
    }
.title h1 span{
    color:#58B883;
    margin-right: 10px;
}
.music-container{
    height:100%;
    margin: 50px 0;
    width:300px;
    max-width:400px;
}
.showcase{
    color:white;
    margin:20px 10px 20px 0px;
    font-size: 22px;
    width:100%;
    text-align: center;
    overflow: hidden;
}
.showcase p{
    margin:5px;
    animation: slide 10s linear infinite;
    animation-play-state: paused;
   
}
.music-container.play .showcase p{
    animation-play-state: running;
}
.showcase :nth-child(2){
    font-weight: bold;
}
.cover{
    border-radius: 50%;
    width: 200px;
    height:200px;
    justify-self: center;
    animation: spin 1s linear infinite;
    animation-play-state: paused;
}
.music-container.play .cover{
    animation-play-state: running;
}
.progress-container{
    width:100%;
    height:5px;
    margin-bottom:20px;
    background: rgba(0,0,0,0.2);
    border-radius: 5px;
}
.progress{
    background-color:#6DF3DA;
    height:100%;
    width:0%;
    transition: width 0.1s linear;
    border-radius: 5px;
}

.controls{
    background: rgba(0,0,0,0.2);
    padding:10px;
    border-radius: 5px;
    width:100%;
    box-shadow:0px 5px 20px #6DF3DA;
    animation: breathe 2s linear infinite;
    animation-play-state: paused;
}
.music-container.play .controls{
    animation-play-state: running;
}
.action-btn{
    border:0;
    background: none;
    color:#6DF3DA;
    font-size:20px;
    margin:0 15px;
}
.action-btn:hover{
   color:#58B883;
}
.action-btn:focus{
   outline:none;
}
.action{
    background: #6DF3DA;
    color:white;
    font-size:22px;
    padding:10px;
    border-radius: 50px;
}
.action:hover{
    background: white;
}
.menu{
   position:absolute;
   left:0;
   top:20;
   z-index: 3;
}
.nav{
   position:absolute;
   left:0;
   top:0;
   padding:30px;
   background: rgba(0,0,0,0.2);
   height: 80vh;
   z-index: 2;
   border-radius: 5px;
   transition:opacity 0.5s linear;
   opacity: 0;
}
.nav ul{
    list-style-type: none;
    text-align: left;
    padding:0;
    margin:0;
    z-index: 2;
}
.nav ul li{
    color:white;
    font-size:22px;
    margin:20px 0;
    font-weight: bold;
    transition: color 0.5s linear;
}
.nav ul li:hover{
    color:#6DF3DA;
}
.nav.playing ul li{
     color:#6DF3DA;
}

/* ANIMATIONS */
@keyframes breathe{
    10%{
        box-shadow:0px 5px 10px #6DF3DA;
    }
    30%{
          box-shadow:0px 5px 20px red;
    }
    50%{
         box-shadow:0px 5px 30px yellow;
    }
    100%{
         box-shadow:0px 5px 40px #6DF3DA;
    }
}
@keyframes slide {
    10%{
         transform: translateX(100%);
    }
    20%{
         transform: translateX(90%);
    }
    30%{
        transform: translateX(80%);
    }
    40%{
         transform: translateX(50%);
    }
    50%{
      transform: translateX(40%);
    }
    60%{
        transform: translateX(30%);
    }
    70%{
         transform: translateX(20%);
    }
    80%{
      transform: translateX(10%);
    }
    90%{
         transform: translateX(0%);
    }
    100%{
       transform: translateX(-100%);
    } 
}
@keyframes spin {
    0%{
        transform: rotate(0deg);
    }
    100%{
        transform: rotate(360deg);
    }
    
}

/* MEDIA QUERIES */
@media (max-width:500px) {
    .nav{
   background: rgba(0,0,0,0.5);
}
    .title h1{
        font-size:35px;
    }
    
}

</style>