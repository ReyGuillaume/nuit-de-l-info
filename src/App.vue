<script setup>
import DocumentComp from "./components/DocumentComp.vue";
import Bilan from "./components/Bilan.vue";

import { ref, onMounted } from 'vue';
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
const maxEnvironnement = ref(0);
const maxFinance = ref(0);
const maxConfort = ref(0);

const minEnvironnement = ref(0);
const minFinance = ref(0);
const minConfort = ref(0);

const pourcentageEnvironnement = ref(0);
const pourcentageFinance = ref(0);
const pourcentageConfort = ref(0);
for (let i = 0; i<tabQuestions.length; i++){
    let maxEnvironnementQuestion = tabQuestions[i].reponses[0].score["environnement"];
    let maxFinanceQuestion = tabQuestions[i].reponses[0].score["finance"];
    let maxConfortQuestion = tabQuestions[i].reponses[0].score["confort"];
    for (let j = 1; j <tabQuestions[i].reponses.length; j++){


        if(tabQuestions[i].reponses[j].score["environnement"] > maxEnvironnementQuestion){
            maxEnvironnementQuestion = tabQuestions[i].reponses[j].score["environnement"];
        }
        if(tabQuestions[i].reponses[j].score["finance"] > maxFinanceQuestion){
            maxFinanceQuestion = tabQuestions[i].reponses[j].score["finance"];
        }
        if(tabQuestions[i].reponses[j].score["confort"] > maxConfortQuestion){
            maxConfortQuestion = tabQuestions[i].reponses[j].score["confort"];
        }
    }
    maxEnvironnement.value += maxEnvironnementQuestion;
    maxFinance.value += maxFinanceQuestion;
    maxConfort.value += maxConfortQuestion;
}
for (let i = 0; i<tabQuestions.length; i++){
    let minEnvironnementQuestion = tabQuestions[i].reponses[0].score["environnement"];
    let minFinanceQuestion = tabQuestions[i].reponses[0].score["finance"];
    let minConfortQuestion = tabQuestions[i].reponses[0].score["confort"];
    for (let j = 1; j <tabQuestions[i].reponses.length; j++){


        if(tabQuestions[i].reponses[j].score["environnement"] < minEnvironnementQuestion){
            minEnvironnementQuestion = tabQuestions[i].reponses[j].score["environnement"];
        }
        if(tabQuestions[i].reponses[j].score["finance"] < minFinanceQuestion){
            minFinanceQuestion = tabQuestions[i].reponses[j].score["finance"];
        }
        if(tabQuestions[i].reponses[j].score["confort"] < minConfortQuestion){
            minConfortQuestion = tabQuestions[i].reponses[j].score["confort"];
        }
    }
    minEnvironnement.value += minEnvironnementQuestion;
    minFinance.value += minFinanceQuestion;
    minConfort.value += minConfortQuestion;
    
}



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
  pourcentageEnvironnement.value = (100 /(maxEnvironnement.value - minEnvironnement.value)) * (tabScore.value[0].value - minEnvironnement.value);
  pourcentageFinance.value = (100 /(maxFinance.value - minFinance.value)) * (tabScore.value[1].value - minFinance.value);
  pourcentageConfort.value = (100 /(maxConfort.value - minConfort.value)) * (tabScore.value[2].value - minConfort.value);
  console.log(pourcentageEnvironnement.value)
  console.log(pourcentageFinance.value)
  console.log(pourcentageConfort.value)


  questionRepondu.push(reponse_id);
  dataQuestion.value = tabQuestions[question_id];
  fin.value = question_id >= tabQuestions.length;
  saut_question(fin, dataQuestion, questionRepondu, question_id)
}


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

console.log(tabScore)
const img = Math.floor(Math.random() * 2) == 0 ? bg1 : bg2;
</script>

<template>
  <div class="back">
    <img :src="fg1" alt="" class="foreground" />
    <img :src="img" alt="" class="background" />
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
</style>
