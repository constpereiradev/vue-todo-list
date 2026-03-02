<script setup>
import { ref, computed, onMounted } from 'vue'

const header = ref('Lista de tarefas')

const items = ref([])
const newItem = ref('')
const highPriority = ref(false)
const newItemLimit = ref(200)

onMounted(() => {
  var localStorageItems = localStorage.getItem('items')
  if(localStorageItems){
    items.value = JSON.parse(localStorageItems)
  }
})

const addItem = () => {

  if (newItem.value.length < 1) {
    alert('O item deve conter um nome!')
    return
  }

  if(newItemCount.value >= newItemLimit.value){
    alert(`O nome do item não pode ultrapassar ${newItemLimit.value} caracteres`)
    return
  }

  var lasItemId = items.value.length == 0 ? 0 : items.value.at(-1).id
  var newItemId = lasItemId + 1

  items.value.push({
    id: newItemId,
    name: newItem.value,
    highPriority: highPriority.value
  })

  localStorage.setItem('items', JSON.stringify(items.value))
}

const mark = (item) => {
  item.marked = true
}

const removeItem = (index) => {
  items.value.splice(index, 1)
}

const newItemCount = computed(() => {
  return newItem.value.length
})

const itemsReversed = computed(() => [...items.value].reverse())

</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
  </div>

  <form v-on:submit.prevent="addItem">
    <input v-model="newItem" type="text"></input>
    <input v-model="highPriority" type="checkbox">Prioridade</input>
    <button v-bind:disabled="newItem.length === 0 || newItem.length >= newItemLimit">Adicionar</button>
  </form>

  {{newItemCount}}/200
  <p v-if="!items.length">Nenhum item cadastrado</p>
  <p v-else>Clique no nome do item para riscar da lista</p>

  <ul> 
    <li v-for="(item, index) in itemsReversed">
      <p>
        <span v-on:click="mark(item)" v-bind:class="{ marked: item.marked, priority: item.highPriority }">{{ item.name }}</span>
        <button v-on:click="removeItem(index)">Remover</button>
      </p> 

    </li>
  </ul>

</template>
