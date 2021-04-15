<template>
<div class="title">
    <h1>Spot on</h1>
     <p>Music for the soul...</p>
</div>

<div class="music-container">
    <div>
        <img src="../assets/img/stay-high.jpeg" alt="" class="cover">
    </div>
    <div class="showcase">
        <p class="music-title">Stay High</p>
        <p class="music-singer">Juice WRLD</p>
    </div>
    <div class="progress-container">
        <div class="progress">
        </div>
    </div>
    <audio src="../assets/Stay_High.mp3"></audio>
    <div class="controls">
        <button class="action-btn"><fas icon="backward"/></button>
        <button class="action-btn action"><fas icon="play"/></button>
        <button class="action-btn"><fas icon="forward"/></button>
    </div>

</div>
</template>

<script>
export default {
    

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

}
.title{
    color:white;
}
.music-container{
    height:100%;
    margin: 50px 0;
    width:100%;
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
.showcase :nth-child(2){
    font-weight: bold;
}
.cover{
    border-radius: 50%;
    justify-self: center;
    animation: spin 1s linear infinite;
    animation-play-state: paused;
}
.progress-container{
    width:100%;
    height:5px;
    margin-bottom:20px;
    background: rgba(0,0,0,0.2);
    border-radius: 5px;
}
.progress{
    background-color:#78E87A;
    height:100%;
    width:10%;
    border-radius: 5px;
}

.controls{
    background: rgba(0,0,0,0.2);
    padding:10px;
    border-radius: 5px;
    width:100%;
    box-shadow:0px 5px 20px #78E87A;
    animation: breathe 1s linear infinite;
    animation-play-state: paused;
}
.action-btn{
    border:0;
    background: none;
    color:#78E87A;
    font-size:20px;
    margin:0 15px;
}
.action-btn:focus{
   outline:none;
}
.action{
    background: #78E87A;
    color:white;
    font-size:22px;
    padding:10px;
    border-radius: 50px;
}

/* ANIMATIONS */
@keyframes breathe{
    10%{
        box-shadow:0px 5px 10px #78E87A;
    }
    30%{
          box-shadow:0px 5px 20px #78E87A;
    }
    50%{
         box-shadow:0px 5px 30px #78E87A;
    }
    100%{
         box-shadow:0px 5px 40px #78E87A;
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

</style>