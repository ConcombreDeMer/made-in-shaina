<template>

    <div class="form-part">
   
        <div class="previous">
            <button v-if="previous" class="button-previous" @click="goBack">←</button>
        </div>
    
        <div class="form-part-content">
            <h1>{{ title }}</h1>
            <slot class="inputs"></slot>
        </div>
    
        <div class="next">
            <button v-if="next" class="button-next" @click="goNext">→</button>
        </div>

    </div>

</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

defineProps<{
    title: string;
    previous : boolean;
    next : boolean;
}>();

const emit = defineEmits(['goBack', 'goNext']);

const goBack = () => {
    console.log('go back');
    emit('goBack');
}

const goNext = () => {
    console.log('go next');
    emit('goNext');
}


</script>

<style scoped>




.form-part {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 100%;    
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
}

.form-part-content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 30%;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

}


.previous, .next {
    width: 5vh;
    height: 5vh;
}

button {
 display: flex;
 height: 6vh;
 width: 6vh;
 align-items: center;
 justify-content: center;
 background-color: #eeeeee4b;
 border-radius: 10px;
 letter-spacing: 1px;
 transition: all 0.2s linear;
 cursor: pointer;
 border: none;
 background: #fff;
 margin: 2vh;
 font-size: 4vh;
 font-weight: lighter;
}

button > svg {
 margin-right: 5px;
 margin-left: 5px;
 font-size: 20px;
 transition: all 0.4s ease-in;
}

button:hover > svg {
 font-size: 1.2em;
 transform: translateX(-5px);
}

button:hover {
 box-shadow: 9px 9px 33px #d1d1d1, -9px -9px 33px #ffffff;
 transform: translateY(-2px);
}
</style>
