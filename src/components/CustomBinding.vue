<script setup lang="ts">
import { defineEmits, defineProps } from 'vue';

const foo = '';

// Parameter der Komponente "CustomBinding"
// <CustomBinding v-model="custom" :foo="foo" :bar="bar"></CustomBinding>
const props = defineProps({
    modelValue: { // v-model
        type: String,
        required: true
    },
    foo: {
        type: String,
        default: 'foo'
    },
    bar: {
        type: Number,
        default: 42
    }
});

const emit = defineEmits(['update:modelValue']);

const sayHello = (event: MouseEvent, message: string) => {

    if ((event) && (event.target))
        console.log((event.target as HTMLInputElement).name);
    console.log(message);
    console.log(props.modelValue);
}

const changeModelValue = (event: Event) => {
    emit('update:modelValue', (event.target as HTMLInputElement).value)
}
</script>

<template>
    <div>
        <input 
            type="text" 
            name="custom"
            :value="modelValue"
            @input="changeModelValue">

        <button name="clickme" @click="sayHello($event, 'Hello World')">Click me!</button>

        <p></p>
    </div>
</template>