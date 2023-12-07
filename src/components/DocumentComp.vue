<script setup>
import { ref } from "vue";
// une question reçu par la page


// defineProps({
//   question: String,
//   
// })

const curId = 2

const question = ref({
    id_question: 1,
    question : "Quel est la bonne réponse ? (A)",
    explication : "A est toujours la meilleur réponse",
    reponses : [{
        id_reponse : 1,
        reponse : "A",
        exemplevar1 : -2
    },{
        id_reponse : 2,
        reponse : "COUCOU",
        exemplevar1 : -2
    },{
        id_reponse : 3,
        reponse : "toto",
        exemplevar1 : -2
    }]
});


</script>

<template>
    <div class="global">
        <div class="document">
            <h2 class="main-text">{{ question.question }}</h2>
            <div>
                <button :class="{ 'active': item.id_reponse == curId }" v-for="item of question.reponses" @click="$emit('testEmit', question.id_question, item.id_reponse)">{{ item.reponse }}</button>
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
.active {
    color: blue;
}
</style>