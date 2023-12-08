<script setup>
import DocumentComp from './components/DocumentComp.vue'
import Bilan from './components/Bilan.vue'

import { ref, onMounted } from 'vue';
import storie from './Stories.json'
import fg1 from '../images/bureau1.png'
import bg1 from '../images/background1.png'
import bg2 from '../images/background2.png'

var tabQuestions = storie.Sarah.questions
var dataQuestion = ref(tabQuestions[0]);


const tabScore = ref([
  { key: 'environnement', value:0 },
  { key: 'finance', value: 0 },
  { key: 'confort', value: 0 }
]);
const fin = ref(false)

function modifScore(question_id, reponse_id){
const question = tabQuestions.find(elt => elt.id_question == question_id)
const reponse = question.reponses.find(elt => elt.id_reponse == reponse_id)
tabScore.value[0].value += reponse.score.environnement;
tabScore.value[1].value += reponse.score.finance;
tabScore.value[2].value += reponse.score.confort;
console.log(tabScore)
dataQuestion.value = tabQuestions[ question_id ];
fin.value = question_id >= tabQuestions.length
}

const img = Math.floor(Math.random() * 2) == 0 ? bg1 : bg2

</script>

<template>
  <div class="back">
    <img :src="fg1" alt="" class="foreground">
    <img :src="img" alt="" class="background">
  </div>
  <DocumentComp @modif-score="modifScore" :question="dataQuestion"></DocumentComp>
  <Bilan v-if="fin" :tabQuestions="tabQuestions" :tabScore="tabScore"></Bilan>

</template>

<style scoped>
.foreground {
  position: absolute;
  width: 100vw;
  height: auto;

  bottom: 0px;
}
.background {
  position: absolute;
  width: 100vw;
  height: auto;
  z-index: -1;

  bottom: 0px;
}
</style>
