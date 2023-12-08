<script setup>
import { ref } from "vue";
const props = defineProps({
    tabScore:Array,
    tabQuestions:Array
})



</script>


<template>
    <div class="global">
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


</style>