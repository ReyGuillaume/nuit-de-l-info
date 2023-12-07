<script setup>
import DocumentComp from './components/DocumentComp.vue'
import { ref } from 'vue';
const tabQuestions = ref(
  [{
    id_question: 1,
    question : "Quel est la bonne réponse ? (A)",
    explication : "A est toujours la meilleur réponse",
    reponses : [{
        id_reponse : 1,
        reponse : "A",
        score : {environnement:1, finance:0, confort:1}
    },{
        id_reponse : 2,
        reponse : "Test",
        score : {environnement:1, finance:0, confort:1}
    },{
        id_reponse : 3,
        reponse : "toto",
        score : {environnement:1, finance:0, confort:1}
      }
    ]},
    {
    id_question: 2,
    question : "Quel est la bonne réponse ? (B)",
    explication : "A est toujours la meilleur réponse",
    reponses : [{
        id_reponse : 1,
        reponse : "B",
        score : {environnement:1, finance:0, confort:1}
    },{
        id_reponse : 2,
        reponse : "B2",
        score : {environnement:1, finance:0, confort:1}
    },{
        id_reponse : 3,
        reponse : "B3",
        score : {environnement:1, finance:0, confort:1}
      }
    ]},
    {
    id_question: 3,
    question : "Quel est la bonne réponse ? (C)",
    explication : "A est toujours la meilleur réponse",
    reponses : [{
        id_reponse : 1,
        reponse : "C",
        score : {environnement:1, finance:0, confort:1}
    },{
        id_reponse : 2,
        reponse : "C2",
        score : {environnement:1, finance:0, confort:1}
    },{
        id_reponse : 3,
        reponse : "C3",
        score : {environnement:1, finance:0, confort:1}
      }
      ]},
  ]);

var dataQuestion = ref(tabQuestions.value[0]);

const tabScore = ref([
  { key: 'environnement', value:0 },
  { key: 'finance', value: 0 },
  { key: 'confort', value: 0 }
]);

function modifScore(question_id, reponse_id){
  const question = tabQuestions.value[question_id];
  const reponse = question.reponses[reponse_id-1];

  tabScore.value[0].value += reponse.score.environnement;
  tabScore.value[1].value += reponse.score.finance;
  tabScore.value[2].value += reponse.score.confort;
  dataQuestion.value = tabQuestions.value[ question_id +1 ];
  console.log( tabScore );
}

// Constante pour le bouton démarrer
const showDocumentComp = ref(false);

// fonction du bouton démarrer
function startDocumentComp() {
  showDocumentComp.value = true;
}

</script>

<template>
  <div class="global" v-if="!showDocumentComp">
    <div class="document">
        <h1>Le Jeux de l'écologie</h1>
        <p>Pour démarrer une partie cliquez sur le boutton</p>
        <button @click="showDocumentComp = true">
          Démarrer
        </button>
    </div>
  </div>

  <DocumentComp
     v-if="showDocumentComp" @testEmit="modifScore" :question="dataQuestion"></DocumentComp>
  
</template>

<style scoped>
</style>
