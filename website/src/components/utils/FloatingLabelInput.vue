<template>

    <div class="floating-label-input">
        <input :id="id" v-model="internalValue" @focus="isFocused = true" @blur="isFocused = false" :type="type"
            :required="required" :class="{ filled: hasContent, focused: isFocused }" />
        <label :for="id" :class="{ 'label-floating': hasContent || isFocused }">
            {{ label }}
        </label>
    </div>

</template>

<script setup lang="ts">

import { defineProps } from 'vue';

const props = defineProps({
    id: String,
    label: String,
    type: {
        type: String,
        default: 'text'
    },
    required: {
        type: Boolean,
        default: false
    },
    modelValue: {
        type: String,
        default: ''
    }
});



</script>

<style scoped></style>