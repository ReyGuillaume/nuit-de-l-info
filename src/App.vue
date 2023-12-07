<script setup>
import HelloWorld from './components/HelloWorld.vue'
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
        reponse : "COUCOU",
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
  //console.log(tabQuestions.value[question_id])
  const question = tabQuestions.value[question_id];
  /*
  if (!question) {
    console.error('Question non trouvée pour l\'ID :', question_id);
    return;
  }
  */
  const reponse = question.reponses[reponse_id-1];
  /*
  if (!reponse) {
    console.error('Réponse non trouvée pour l\'ID :', reponse_id);
    return;
  }
  */
  tabScore.value[0].value += reponse.score.environnement;
  tabScore.value[1].value += reponse.score.finance;
  tabScore.value[2].value += reponse.score.confort;
  dataQuestion.value = tabQuestions.value[ question_id +1 ];
  console.log( tabScore );
}
</script>

<template>
  <DocumentComp @modif-score="modifScore" :data="dataQuestion"></DocumentComp>
</template>

<style scoped>
</style>
