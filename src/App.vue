<script setup>
import {ref, computed} from 'vue'

let i = ref(0)
const color = ref(0)

const increment = () =>{
 i.value++
}

const decrease = () =>{
  i.value--
}

let disabled = ref(false)

const counterColor = computed(()=>{
  if(i.value > 0) return 'positivo'
  if(i.value < 0) return 'negativo'
  if(i.value === 0) return 'cero'
})

const colorMethod= () =>{
  if(i.value > 0) return 'positivo'
  if(i.value < 0) return 'negativo'
  if(i.value === 0) return 'cero'
}

let Favs = ref([])

const reset = () =>{
  i.value= 0
}

const resetFavs = () =>{
  Favs.value.length=0
}
const add = (i) =>{
  disabled = Favs.value.includes(i);
  if (!disabled) Favs.value.push(i)
}

const blockingAdd = computed(()=>{
  const block = Favs.value.includes(i.value);
  return block || block === 0
})


</script>


<template>
  <h2 :class="counterColor">{{i}}</h2>
<button @click="increment">Increment</button>
  <br>
  <button @click="decrease">Decrease</button>
  <br>
  <button @click="reset">Reset</button>
  <br>
  <button @click="resetFavs">Reset Favs</button>
  <br>
  <button @click="add(i)" :disabled="blockingAdd">add</button>
  <br>
<ul>
  <template v-for="(number, index) in Favs" :key="index">
    <li >{{number}}</li>
  </template>
</ul>
</template>

<style>
h1{color:red}

.negativo{color:red}

.positivo{color:green}

.cero{color:blue}
</style>
