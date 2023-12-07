<script setup>
import DocumentComp from './components/DocumentComp.vue'

function testEmit(question_id, reponse_id){
  console.log( question_id, reponse_id)
}
</script>

<template>
  <DocumentComp @test-emit="testEmit"></DocumentComp>
</template>

<style scoped>
</style>
