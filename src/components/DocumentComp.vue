<script setup>
import { ref } from "vue";
// une question reçu par la page


// defineProps({
//   question: String,
//   
// })

const question = ref({
    id_question: 1,
    question : "Quel est la bonne réponse ? (A)",
    explication : "A est toujours la meilleur réponse",
    reponses : [{
        id_reponse : 1,
        reponse : "A",
        exemplevar1 : -2
    }]
});

// function choisirReponse(id_reponse){
//     $emit('CHANGEME', question)
// }



</script>

<template>
    <div class="global">
        <div class="document">
            <h2 class="main-text">{{  }}</h2>
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
}
.document {
    width: calc(210 * .25vh);
    min-height: calc(297 * .25vh);
    background-color: #fffbfb;
}
</style>