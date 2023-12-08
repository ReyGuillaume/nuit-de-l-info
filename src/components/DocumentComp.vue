<script setup>

defineProps({
    question: Object
})

var day = 0
function goNextDay() {
    let global = document.querySelector('.global')  
    let blackscreen = document.querySelector('.blackscreen')
    day++
    blackscreen.style.zIndex = '3'
    blackscreen.classList.add('show')
    global.style.display = 'none'
    setTimeout(() => {
        blackscreen.classList.remove('show')
        global.style.display = 'flex'
    }, 2000)
    setTimeout(() => {
        blackscreen.style.zIndex = '1'
    }, 4800)
    // wait 3s before removing z-index

}
</script>

<template>
     <div v-if="question">
        <div class="blackscreen">
            <h1>Jour {{ day }}</h1>
        </div>
        <div class="global">
            <div class="document">
                <h2 class="main-text" v-html="question.question"></h2>

                <div class="reponses">
                    <div class="reponse" v-for="item of question.reponses" :key="item.id" >
                        <button
                        @click="goNextDay(); $emit('modifScore', question.id_question, item.id_reponse)">
                            {{ item.reponse }}
                        </button>
                    </div>
                </div>
            
            </div>
        </div>
    </div>
</template>

<style>
.blackscreen {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: black;
    color: white;

    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1;
    font-size: 5em;

    opacity: 0;
    transition: opacity 3s;
}

.blackscreen.show {
    opacity: 1;
}



.global {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: onHoverIcon .5s;
    z-index: 3;
}

.document {
    width: calc(250 * .25vh);
    min-height: calc(297 * .25vh);
    background-color: #fffbfb;
    background-color: rgba(238, 228, 228, 0.896);
    border-radius: 8%;
    padding: 35px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

}

.main-text {
    color: #025627;
}

.reponses {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: space-around;
    align-items: center;

    padding-top: 1em;

}

.reponse {
    align-items: center;
    position: relative;
    width: 8rem;
    margin-bottom: 1rem;

width: 100%;

}

.reponse button {
    background-color: #04AA6D; 
    color: white;
    border: 2px solid #04AA6D;
    border-radius: 4px;
    /*
    padding: 15px 32px;
    */

    padding: 1em;

    text-align: center;
    text-decoration: none;
    font-size: 16px;
    transition-duration: 0.4s;
    width: 100%;
    font-family: 'Courier New', Courier, monospace;

    word-break: break-word;

}

.reponse button:hover {
  background-color: rgba(238, 228, 228, 0.434);
  color: #04AA6D;
  border: 2px solid #04AA6D;
  cursor: pointer;
}


@keyframes onHoverIcon {
    0% {
        top: -100%;
        left: -50%;
        transform: rotate(45deg);
    }
    50% {
        top: 15%;
        left: 15%;
    }
    75% {
        top: -5%;
        left: -5%;
    }
    100% {
        top: 0;
        left: 0;
    }
}
</style>