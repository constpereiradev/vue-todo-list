<script setup>
import { ref, computed, onMounted, watch } from 'vue'
import TodoHeader from './components/Header.vue'

const items = ref([])
const newItem = ref('')
const highPriority = ref(false)
const newItemLimit = ref(200)
let darkMode = ref(false)
const showMarkedItems = ref(false)

onMounted(() => {
  let localStorageItems = getLocalStorageData('items')
  if (localStorageItems) {
    items.value = JSON.parse(localStorageItems)
  }

  let localStorageDarkMode = getLocalStorageData('dark-mode')
  if (localStorageDarkMode) {
    darkMode.value = JSON.parse(localStorageDarkMode)
  }
})

const getLocalStorageData = (item) => {
  return localStorage.getItem(item)
}

const addItem = () => {

  if (newItem.value.length < 1) {
    alert('O item deve conter um nome!')
    return
  }

  if (newItemCount.value >= newItemLimit.value) {
    alert(`O nome do item não pode ultrapassar ${newItemLimit.value} caracteres`)
    return
  }

  let lasItemId = items.value.length == 0 ? 0 : items.value.at(-1).id
  let newItemId = lasItemId + 1

  items.value.push({
    id: newItemId,
    name: newItem.value,
    highPriority: highPriority.value,
    marked: false
  })

  newItem.value = ''
  highPriority.value = false
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

const markedItems = computed(() => {
  if (showMarkedItems.value) {
    return items.value.filter((items) => items.marked == true)
  }

  return items.value
})

/**
Observa todas as mudanças feitas nos items.
O deep considera todas as mudanças internas (push, replice, etc)*/
watch(items, (newItemsValue) => {
  localStorage.setItem('items', JSON.stringify(newItemsValue))
}, { deep: true })

watch(darkMode, (newDarkModeValue) => {
  localStorage.setItem('dark-mode', JSON.stringify(newDarkModeValue))
})

const handleDarkMode = (darkModeValue) => {
  darkMode.value = darkModeValue
}

</script>

<template>
  <div class="todolist" :class="{ darkMode: darkMode }">

    <TodoHeader v-on:dark-mode="$event => handleDarkMode($event)"></TodoHeader>

    <form v-on:submit.prevent="addItem">
      <input v-model="newItem" type="text"></input>
      <input v-model="highPriority" type="checkbox">Prioridade</input>
      <input v-on:click="showMarkedItems = !showMarkedItems" type="checkbox">Riscados</input>
      <button v-bind:disabled="newItem.length === 0 || newItem.length >= newItemLimit">Adicionar</button>
    </form>

    {{ newItemCount }}/200
    <br>
    <p v-if="!markedItems.length">Nenhum item cadastrado</p>
    <p v-else>Clique no nome do item para riscar da lista</p>

    <ul>
      <li v-for="(item, index) in markedItems" :key=item.id>
        <p>
          <span v-on:click="mark(item)" v-bind:class="{ marked: item.marked, priority: item.highPriority }">{{ item.name
            }}</span>
          <button v-on:click="removeItem(index)">Remover</button>
        </p>

      </li>
    </ul>
  </div>

</template>
