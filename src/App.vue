<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { onMounted, reactive, ref, type Ref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'
import CustomBinding from './components/CustomBinding.vue';
import type { Person } from './models/Person';
import ContactFormVue from './components/ContactForm.vue';

let person = reactive<Person>({
  firstName: 'Larissa',
  lastName: 'Römer',
  age: 28,
});

const persons = reactive<Person[]>([
  { firstName: 'Larissa', lastName: 'Römer', age: 28 },
  { firstName: 'Manuel', lastName: 'Kübler', age: 34 },
]);

const contact = reactive<Person>({
    firstName: '',
    lastName: '',
    email: ''
});

const message: Ref<string> = ref('Hello Vue 3 Grundkurs');

  onMounted(() => {
    const personString = localStorage.getItem('person');
    console.log(personString);
    if (personString) {
      person = JSON.parse(personString);
    }
  })
const changeMessage = () => {
  message.value = 'Message changed';
};

const changeAge = (value: number = 1) => {
  person.age = person.age! + value;
  localStorage.setItem('person', JSON.stringify(person))
};

// Custom Two-way-binding
const custom = ref('Custom Two-way-binding');

const customDefault = ref('');

</script>

<template>
  <h1>Vue 3 Grundkurs</h1>
  <HelloWorld msg="Hello World" :custom="custom" :contact="contact"></HelloWorld>
  <button @click="changeMessage">Change Message</button>


  <!-- Kurzform -->
  <input v-model="customDefault" />

  <!-- Langform Variante 1 -->
  <input 
    v-bind:value="customDefault"
    v-on:input="event => customDefault = (event.target as HTMLInputElement).value"
  />

  <!-- Langform Variante 2 -->
  <input 
    :value="customDefault"
    @input="event => customDefault = (event.target as HTMLInputElement).value"
  />



  {{ person.firstName }} {{ person.lastName }} is {{ person.age }} years old.
  <button @click="() => changeAge()">Change Age</button>
  
  <div v-for="person in persons" :key="person.firstName">
    {{ person.firstName }}
  </div>

  <p></p>

  <CustomBinding v-model="custom"></CustomBinding>
  <p>{{ custom }}</p>

  <ContactFormVue v-model="contact"></ContactFormVue>

  <pre>App.contact: {{ contact }}</pre>

</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
