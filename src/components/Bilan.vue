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

console.log(minEnvironnement.value)
console.log(minFinance.value)
console.log(minConfort.value)
console.log(maxEnvironnement.value)
console.log(maxFinance.value)
console.log(maxConfort.value)

pourcentageEnvironnement.value = (100 /(maxEnvironnement.value - minEnvironnement.value)) * (props.tabScore[0].value + minEnvironnement.value);
pourcentageFinance.value = (100 /(maxFinance.value - minFinance.value)) * (props.tabScore[1].value + minFinance.value);
pourcentageConfort.value = (100 /(maxConfort.value - minConfort.value)) * (props.tabScore[2].value + minConfort.value);
console.log(pourcentageEnvironnement.value)
console.log(pourcentageFinance.value)
console.log(pourcentageConfort.value)

// pourcentageFinance.value = ;
// pourcentageConfort.value = ;
</script>


<template>
    <div class="global">
        <div class="document">
            <h2 class="main-text"> Bilan </h2>
            <div>
                <h2> Pourcentage d'environnement : {{ pourcentageEnvironnement }}</h2>
                <h2> Pourcentage de finance : {{ pourcentageFinanceFinance }}</h2>
                <h2> Pourcentage de confort : {{ pourcentageConfort }}</h2>

                <h2 v-for="item of tabScore"> {{ item.key }} : {{ item.value }}</h2>
            </div>
        </div>
    </div>
</template>


<style scoped>
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