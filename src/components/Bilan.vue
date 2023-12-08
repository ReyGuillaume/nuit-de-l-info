<script setup>
import { ref } from "vue";
const props = defineProps({
    tabScore:Array,
    tabQuestions:Array
})
const maxEnvironnement = ref(0);
const maxFinance = ref(0);
const maxConfort = ref(0);

const minEnvironnement = ref(0);
const minFinance = ref(0);
const minConfort = ref(0);

const pourcentageEnvironnement = ref(null);
const pourcentageFinance = ref(null);
const pourcentageConfort = ref(null);
for (let i = 0; i<props.tabQuestions.length; i++){
    let maxEnvironnementQuestion = props.tabQuestions[i].reponses[0].score["environnement"];
    let maxFinanceQuestion = props.tabQuestions[i].reponses[0].score["finance"];
    let maxConfortQuestion = props.tabQuestions[i].reponses[0].score["confort"];
    for (let j = 1; j <props.tabQuestions[i].reponses.length; j++){


        if(props.tabQuestions[i].reponses[j].score["environnement"] > maxEnvironnementQuestion){
            maxEnvironnementQuestion = props.tabQuestions[i].reponses[j].score["environnement"];
        }
        if(props.tabQuestions[i].reponses[j].score["finance"] > maxFinanceQuestion){
            maxFinanceQuestion = props.tabQuestions[i].reponses[j].score["finance"];
        }
        if(props.tabQuestions[i].reponses[j].score["confort"] > maxConfortQuestion){
            maxConfortQuestion = props.tabQuestions[i].reponses[j].score["confort"];
        }
    }
    maxEnvironnement.value += maxEnvironnementQuestion;
    maxFinance.value += maxFinanceQuestion;
    maxConfort.value += maxConfortQuestion;
}

for (let i = 0; i<props.tabQuestions.length; i++){
    let minEnvironnementQuestion = props.tabQuestions[i].reponses[0].score["environnement"];
    let minFinanceQuestion = props.tabQuestions[i].reponses[0].score["finance"];
    let minConfortQuestion = props.tabQuestions[i].reponses[0].score["confort"];
    for (let j = 1; j <props.tabQuestions[i].reponses.length; j++){


        if(props.tabQuestions[i].reponses[j].score["environnement"] < minEnvironnementQuestion){
            minEnvironnementQuestion = props.tabQuestions[i].reponses[j].score["environnement"];
        }
        if(props.tabQuestions[i].reponses[j].score["finance"] < minFinanceQuestion){
            minFinanceQuestion = props.tabQuestions[i].reponses[j].score["finance"];
        }
        if(props.tabQuestions[i].reponses[j].score["confort"] < minConfortQuestion){
            minConfortQuestion = props.tabQuestions[i].reponses[j].score["confort"];
        }
    }
    minEnvironnement.value += minEnvironnementQuestion;
    minFinance.value += minFinanceQuestion;
    minConfort.value += minConfortQuestion;
    
}



pourcentageEnvironnement.value = (100 /(maxEnvironnement.value - minEnvironnement.value)) * (props.tabScore[0].value - minEnvironnement.value);
pourcentageFinance.value = (100 /(maxFinance.value - minFinance.value)) * (props.tabScore[1].value - minFinance.value);
pourcentageConfort.value = (100 /(maxConfort.value - minConfort.value)) * (props.tabScore[2].value - minConfort.value);

</script>


<template>
    <div class="global">
        <div class="document">
            <h2 class="main-text"> Bilan </h2>
            <div>
                <h2>environnement</h2>
                <div id="Progress_Status">
                    <div :style="{width: 'clamp(0%,' + pourcentageEnvironnement + '%, 100%)'}" id="myprogressBar" ></div>
                </div>
                <h2>finance</h2>
                <div id="Progress_Status">
                    <div :style="{width: 'clamp(0%,' + pourcentageFinance + '%, 100%)'}" id="myprogressBar"></div>
                </div>
                <h2>confort</h2>
                <div id="Progress_Status">
                    <div :style="{width: 'clamp(0%,' + pourcentageConfort + '%, 100%)'}" id="myprogressBar"></div>
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>

#Progress_Status {
  width: 100%;
  background-color: #ddd;
}
  
#myprogressBar {
  width: 2%;
  height: 20px;
  background-color: #4CAF50;
}

</style>