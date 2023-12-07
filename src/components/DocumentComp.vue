<script setup>

// une question reçu par la page

// des réponses 

</script>

<template>
    <div class="global">
        <div class="document">
            <h2 class="main-text">{{  }}</h2>
        </div>
    </div>
</template>

<style>
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
}
</style>