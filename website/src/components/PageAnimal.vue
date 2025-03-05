<template>

    <div>
        <h1>Votre animal</h1>

        <FloatingLabelInput class="name" v-model="form.name" label="Nom"/>

        <button>Next</button>

    </div>


</template>

<script setup lang="ts">
import FloatingLabelInput from './utils/FloatingLabelInput.vue';
import { ref } from 'vue';

const form = ref({
    name: '',
});

</script>

<style scoped>


</style>