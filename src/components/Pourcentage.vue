<script setup>
import { ref } from "vue";
const props = defineProps(["pourcentageEnvironnement", "pourcentageFinance", "pourcentageConfort"])
console.log("ezaeaz")
console.log(props.pourcentageEnvironnement)
console.log(props.pourcentageFinance)
console.log(props.pourcentageConfort)


</script>


<template>
    <div class="Pourcentage">
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
</template>


<style scoped>

.Pourcentage{
    position: absolute;
    z-index: 40;
    right: 13rem;
    bottom:8rem

}
#Progress_Status {
  width: 100%;
  background-color: #ddd;
}
  
#myprogressBar {
  width: 2%;
  height: 20px;
  background-color: #4CAF50;
}
h2{
    color: white
}

</style>