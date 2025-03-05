<template>

    <div class="floating-label-input">
        <input :id="id" v-model="internValue" @focus="handleFocus" @blur="handleBlur" :type="type"
            :required="required" :class="{ filled: hasContent, focused: isFocused }" />
        <label :for="id" :class="{ 'label-floating': hasContent || isFocused }">
            {{ label }}
        </label>
    </div>

</template>

<script setup lang="ts">

import { defineProps, defineEmits, watch } from 'vue';
import { ref } from 'vue';

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
    },
});

const init = () => {
    internValue.value = props.modelValue;
    if (internValue.value.length > 0) {
        isFocused.value = true;
    }
}

const internValue = ref(props.modelValue);
const isFocused = ref(false);

const emit = defineEmits({
    'update:modelValue': (value: string) => {
        return typeof value === 'string';
    }
});

watch(internValue, (value) => {
    emit('update:modelValue', value);
});

const hasContent = () => internValue.value.length > 0;

const handleFocus = () => {
    isFocused.value = true;
}

const handleBlur = () => {
    if (!hasContent()) {
        isFocused.value = false;
    }
}

init();

</script>

<style scoped>

.floating-label-input {
    position: relative;
    margin: 1vh 0;
    padding: 1vh 1vw;
    background-color: #EFEFEF;
    width: 100%;
    height: 5vh;
    border-radius: 10px;
}

.floating-label-input input {
    width: 100%;
    padding: 12px 12px 12px 12px;
    font-size: 2vh;
    border: none;
    border-radius: 4px;
    outline: none;
    background-color: transparent;
}



.floating-label-input label {
    position: absolute;
    top: 50%;
    left: 1vw;
    transform: translateY(-50%);
    font-size: 2vh;
    pointer-events: none;
    transition: all 0.3s ease;
    font-weight: lighter;
}

.floating-label-input input.focused+label {
    top: 15px;
    left: 10px;
    padding: 0 4px;
    font-size: 1.2vh;
}


</style>