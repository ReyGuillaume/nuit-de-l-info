<script setup>
import DocumentComp from './components/DocumentComp.vue'
import { ref, onMounted } from 'vue';
import storie from './Stories.json'

var tabQuestions = storie.Sarah.questions
var dataQuestion = ref(tabQuestions[0]);


const tabScore = ref([
  { key: 'environnement', value:0 },
  { key: 'finance', value: 0 },
  { key: 'confort', value: 0 }
]);

function modifScore(question_id, reponse_id){
const question = tabQuestions.find(elt => elt.id_question == question_id)
const reponse = question.reponses.find(elt => elt.id_reponse == reponse_id)
tabScore.value[0].value += reponse.score.environnement;
tabScore.value[1].value += reponse.score.finance;
tabScore.value[2].value += reponse.score.confort;
dataQuestion.value = tabQuestions[ question_id ];
}
</script>

<template>
  <DocumentComp @modif-score="modifScore" :question="dataQuestion"></DocumentComp>
</template>

<style scoped>
</style>
