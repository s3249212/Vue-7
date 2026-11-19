<script setup>
import { ref, computed } from 'vue';
const people = ref([
  {name: 'Jan', age: 12},
  {name: 'Piet', age: 20}
]);
const newName = ref('');
const newAge = ref(0);
function addPerson(){
  people.value.push({name: newName.value, age: newAge.value});
  newName.value = '';
  newAge.value = 0;
}
const children = computed(() => people.value.filter(e => e.age < 18));
const adults = computed(() => people.value.filter(e => e.age >= 18));
const totalPeople = computed(() => people.value.length);
const numberOfChildren = computed(() => children.value.length);
</script>

<template>
<input v-model="newName">
<input v-model.number="newAge">
<button @click="addPerson">Toevoegen</button>
<h2>Personenlijsten</h2>
<h3>Iedereen</h3>
<ul>
  <li v-for="(person, index) in people" :key="index">{{ person.name }}: {{ person.age }}</li>
</ul>
<h3>Kinderen</h3>
<ul>
  <li v-for="(person, index) in children" :key="index">{{ person.name }}: {{ person.age }}</li>
</ul>
<h3>Volwassenen</h3>
<ul>
  <li v-for="(person, index) in adults" :key="index">{{ person.name }}: {{ person.age }}</li>
</ul>
<h2>Statistieken</h2>
Aantal kinderen: {{ numberOfChildren }}
Totaal aantal personen: {{  totalPeople }}
</template>
