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

const messageFinal = ref(null);

if (pourcentageEnvironnement.value < pourcentageFinance.value && pourcentageEnvironnement.value < pourcentageConfort.value){
    let random = Math.floor(Math.random()*5);
    if (random == 0){
        messageFinal.value = "Changer son mode de chauffage est une bonne chose mais il faut faire attention à ce que l'on choisit. Le fioul est une énergie fossile qui pollue beaucoup. L'isolation est un moyen efficace de réduire sa consommation d'énergie sans changer de mode de chauffage."
    }
    else if (random == 1){
        messageFinal.value = "La consommation de viande est très polluante. Ne pas en manger est quelque chose d'illusoire mais en manger moins est un bon début."
    }
    else if (random == 2){
        messageFinal.value = "Le passage à une voiture électrique est une bonne solution, sous certaines conditions : la voiture doit remplacer une voiture thermique de même gabarit et puissance, et elle doit être utilisée le plus longtemps possible."
    }
    else if (random == 3){
        messageFinal.value = "La température idéale pour une pièce est de 19°C. Chaque degré supplémentaire consomme 7% d'énergie en plus."
    }
    else if (random == 4){
        messageFinal.value = "Le covoiturage ou le prêt de voiture est une bonne solution pour réduire son impact environnemental. Utiliser un véhicule uniquement lorsqu'on en a besoin est à la fois écologique et économique."
    }
    else{
        messageFinal.value = "L'impact digital sur les émissions de gaz à effet de serre représente 4% des émissions mondiales. Trier ses mails est un premier pas pour réduire son impact numérique."
    }
}
else if (pourcentageFinance.value < pourcentageEnvironnement.value && pourcentageFinance.value < pourcentageConfort.value){
    messageFinal.value = "Bravo votre score d'écologie n'est pas le pire !"
}
else{
    messageFinal.value = "Bravo votre score d'écologie n'est pas le pire !"
}
</script>


<template>
    <div class="global">
        <div class="document">
            <h2 class="main-text"> Bilan </h2>
            <h2>{{ messageFinal }}</h2>
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
.global {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    animation: onHoverIcon .5s;
    word-break: break-all;

}
.document {
    width: calc(250 * .25vh);
    min-height: calc(297 * .25vh);
    background-color: #fffbfb;
    background-color: rgba(238, 228, 228, 0.896);
    border-radius: 8%;
    padding: 35px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;

}

.main-text {
    color: #025627;
}

</style>