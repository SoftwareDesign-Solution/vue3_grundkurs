<script setup lang="ts">
import { defineEmits, defineProps, reactive, ref, type PropType } from 'vue';
import type { Person } from '../models/Person';

const props = defineProps({
    modelValue: {
        type: Object as PropType<Person>,
        required: true
    }
});

const value = ref(0);

const firstNameValue = ref('');
const lastNameValue = ref('');

const person = reactive({
    firstName: '',
    lastName: '',
    email: ''
});
</script>

<template>
    <div>
        <div>
            <label for="firstName">Vorname:</label>
            <input type="text" name="firstName" v-model="props.modelValue.firstName">
        </div>
        <div>
            <label for="lastName">Nachname:</label>
            <input type="text" name="lastName" v-model="person.lastName">
        </div>
        <div>
            <label for="email">E-Mail:</label>
            <input type="text" name="email" v-model="person.email">
        </div>
        <div>
            <button type="submit">Absenden</button>
        </div>
        <pre>
            ContactForm.person: {{ person }}
        </pre>
        <pre>
            ContactForm.modelValue: {{ modelValue }}
        </pre>
    </div>
</template>