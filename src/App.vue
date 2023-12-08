<script setup>
import DocumentComp from './components/DocumentComp.vue'
import { ref, onMounted, onUnmounted } from 'vue';
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

function modifScore(question_id, reponse_id){
const question = tabQuestions.find(elt => elt.id_question == question_id)
const reponse = question.reponses.find(elt => elt.id_reponse == reponse_id)
tabScore.value[0].value += reponse.score.environnement;
tabScore.value[1].value += reponse.score.finance;
tabScore.value[2].value += reponse.score.confort;
dataQuestion.value = tabQuestions[ question_id ];
}

const img = Math.floor(Math.random() * 2) == 0 ? bg1 : bg2

const lampOn = ref(false);

function toogleLamp(){
  if (window.innerWidth >= 1500 && window.innerHeight >= 700){
    lampOn.value = !lampOn.value;
  }
}

onMounted(() => {
    window.addEventListener('resize', ()=>{lampOn.value = false});
  });

onUnmounted(()=>{
  window.addEventListener('resize', ()=>{lampOn.value = false});
})
</script>

<template>
  
  <div class="back">
    <div id="lamp" @click="toogleLamp"></div>
  <div v-if="lampOn" class="lampon"></div>
    <img :src="fg1" alt="" class="foreground">
    <img :src="img" alt="" class="background">
  </div>
  <DocumentComp @modif-score="modifScore" :question="dataQuestion"></DocumentComp>
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

#lamp{
  position: absolute;
  width: 2rem;
  height: 2rem;
  left: 9.3rem;
  bottom: 10rem;
  z-index: 10;
}

.lampon {
  position: absolute;
  background: radial-gradient(circle at 50% 50%, rgba(255, 255, 0, 1) 0%, rgba(175, 212, 0, 0) 40%, rgba(229, 238, 130, 0) 50%);
  width: 20rem;
  height: 20rem;
  left: 0.7rem;
  bottom: 15rem;
  z-index: 5;
}

</style>
