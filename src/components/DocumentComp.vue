<script setup>
import { ref } from "vue";
// une question reçu par la page


defineProps({
  question: Object
})


// const question = ref({
//     id_question: 1,
//     question : "Quel est la bonne réponse ? (A)",
//     explication : "A est toujours la meilleur réponse",
//     reponses : [{
//         id_reponse : 1,
//         reponse : "A",
//         exemplevar1 : -2
//     },{
//         id_reponse : 2,
//         reponse : "COUCOU",
//         exemplevar1 : -2
//     },{
//         id_reponse : 3,
//         reponse : "toto",
//         exemplevar1 : -2
//     }]
// });



</script>

<template>
    <div class="global">
        <div class="document">
            <h2 class="main-text">{{ question.question }}</h2>


            <div class="reponses">
                <div class="reponse" v-for="item of question.reponses" :key="item.id" >
                    <button
                    @click="$emit('testEmit', question.id_question, item.id_reponse)">
                        {{ item.reponse }}
                    </button>
                </div>
            </div>
         
        </div>
    </div>
</template>

<style>
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
}
.document {
    width: calc(210 * .25vh);
    min-height: calc(297 * .25vh);
    background-color: #fffbfb;
    padding: 35px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.reponses {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.reponse {
    align-items: center;
    position: relative;
    width: 8rem;
    margin-bottom: 1rem;

}

.reponse button {
    background-color: #04AA6D; 
    color: white;
    border: 2px solid #04AA6D;
    border-radius: 4px;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    font-size: 16px;
    transition-duration: 0.4s;
    width: 100%;

}

.reponse button:hover {
  background-color: white;
  color: #04AA6D;
  border: 2px solid #04AA6D;
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