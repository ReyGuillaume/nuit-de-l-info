<script setup>

import DocumentComp from './components/DocumentComp.vue'
import Bilan from "./components/Bilan.vue";
import { ref, onMounted, onUnmounted } from 'vue';

import storie from './Stories.json'
import fg1 from '../images/bureau1.png'
import bg1 from '../images/background1.png'
import bg2 from '../images/background2.png'
import bg3 from '../images/bg3.png'
import bg4 from '../images/bg4.png'
import bg5 from '../images/bg5.png'
import bg6 from '../images/bg6.png'

var tabQuestions = storie.Sarah.questions;
var dataQuestion = ref(tabQuestions[0]);
var questionRepondu = [];

const tabScore = ref([
  { key: "environnement", value: 0 },
  { key: "finance", value: 0 },
  { key: "confort", value: 0 },
]);
const fin = ref(false);

// Modifie le score
function modifScore(question_id, reponse_id) {
  const question = tabQuestions.find((elt) => elt.id_question == question_id);
  const reponse = question.reponses.find((elt) => elt.id_reponse == reponse_id);

  // modification des score
  tabScore.value[0].value += reponse.score.environnement;
  tabScore.value[1].value += reponse.score.finance;
  tabScore.value[2].value += reponse.score.confort;

  questionRepondu.push(reponse_id);
  dataQuestion.value = tabQuestions[question_id];
  fin.value = question_id >= tabQuestions.length;
  dataQuestion.value.reponses = saut_reponse(dataQuestion, questionRepondu)
  saut_question(fin, dataQuestion, questionRepondu, question_id)
}



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

function saut_question(fin, dataQuestion, questionRepondu, question_id){
  var require_find = false;
  var i = 1;
  while (!require_find && !fin.value) {
    if (dataQuestion.value.require != null) {
      if (!questionRepondu.find((elt) => elt == dataQuestion.value.require)) {
        dataQuestion.value = tabQuestions[question_id + i];
      } else {
        require_find = true;
      }
    } else {
      require_find = true;
    }
    fin.value = question_id + i >= tabQuestions.length;
    i++;
  }
}

function arrayRemove(arr, value) { 
  let new_arr = []
  for (var i in arr) {
    if (arr[i] != value) {
      new_arr.push(arr[i])
    }
  }
  return new_arr
} 

function saut_reponse(dataQuestion, questionRepondu){
  var reponse_arr = []
    for (var reponse in dataQuestion.value.reponses) {
      var requiredReponse = dataQuestion.value.reponses[reponse].require
      if (requiredReponse != null) {
        if (questionRepondu.find((elt) => elt == requiredReponse)) {
          reponse_arr.push(dataQuestion.value.reponses[reponse])
        }
      } else {
        reponse_arr.push(dataQuestion.value.reponses[reponse])
      }
    }
    return reponse_arr
}

const img = Math.floor(Math.random() * 2) == 0 ? bg1 : bg2;

</script>

<template>
  
  <div class="back">
    <div id="lamp" @click="toogleLamp"></div>
    <div v-if="lampOn" class="lampon"></div>
    <img :src="fg1" alt="" class="foreground">
    <img :src="img" alt="" class="background">
  </div>
  <DocumentComp
    @modif-score="modifScore"
    :question="dataQuestion"
  ></DocumentComp>
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
