<template>
  <div id="shopping-list">
    <h1>{{ header }}</h1>
    Priority: 
    <label>
      <input type="checkbox" v-model="newItemHighPriority">
      High Priority
    </label>
    <input type="text" maxLength="50" placeholder="Add an item" v-model.trim="newItem" @keydown.enter="addItem">
    <span>
      {{caracterCount}}/50
    </span>
    <!-- <label>
      <input type="radio" v-model="newItemPriority" value="low">
      Low
    </label>
    <label>
      <input type="radio" v-model="newItemPriority" value="high">
      High
    </label> -->
    <ul >
      <li
        v-for="({id, label, high, purchased}, i) in items"
        :key="i"
        :style="high ? 'color: red' : ''"
        :class="{strikeout: purchased}"
        @click="changePu(purchased, id)"
      >
        {{label}}
      </li>
    </ul>
    <p v-if="items.length === 0">Nothing here!</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
const header = ref('Shopping Lisp App')
const items = ref([])
const newItem = ref('')
const newItemHighPriority = ref(false)

const caracterCount = computed (() => {
  return newItem.value.length
})

const addItem = () => {
  items.value.push({id: items.value.length + 1, label: newItem.value, high: newItemHighPriority.value, purchased: false})
  newItem.value = ''
  newItemHighPriority.value = false
}

const changePu = (purchased, id) => {
  items.value.find(item => item.id === id ? item.purchased = !purchased : '')
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
