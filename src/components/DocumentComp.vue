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


</script>
<template>
    <div>
        Je suis un document
        <button @click="$emit('testEmit', question.id_question, id_reponse)">J'envoie un emit</button>
    </div>
</template>
<style></style>