<script setup>
import { ref, computed, onMounted, watch } from 'vue'

const header = ref('Lista de tarefas')

const items = ref([])
const newItem = ref('')
const highPriority = ref(false)
const newItemLimit = ref(200)
const darkMode = ref(false)
const showMarkedItems = ref(false)
const darkModeIconUrl = 'data:image/png;base64,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'

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

</script>

<template>
  <div class="todolist" :class="{ darkMode: darkMode }">

    <div class="header">
      <h1>{{ header }}</h1>
      <img v-on:click="darkMode = !darkMode" style="width: 20px;" :src="darkModeIconUrl" alt="Icone de dark mode" />
    </div>

    <form v-on:submit.prevent="addItem">
      <input v-model="newItem" type="text"></input>
      <input v-model="highPriority" type="checkbox">Prioridade</input>
      <input v-on:click="showMarkedItems = !showMarkedItems" type="checkbox">Riscados</input>
      <button v-bind:disabled="newItem.length === 0 || newItem.length >= newItemLimit">Adicionar</button>
    </form>

    {{ newItemCount }}/200
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
