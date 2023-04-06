<script setup lang="ts">
import { ref } from 'vue'
import ChildComponent from './ChildComponent.vue'

const parentSum = ref<number>(0)

function handleChildAdding(val: number) {
  alert(`Pai recebeu emit do filho e irá adicionar ${val} ao parentSum`)
  parentSum.value += val
}
</script>

<template>
  <main>
    <h1>Pai</h1>
    <div class="childRow">
      <ChildComponent
        childName="Maria"
        :childValue="3"
        @childAdding="handleChildAdding"
        :parentSum="parentSum"
      />
      <ChildComponent
        childName="João"
        :childValue="10"
        @childAdding="handleChildAdding"
        :parentSum="parentSum"
      />
      <ChildComponent
        childName="Subtração"
        :childValue="1"
        :parentSum="parentSum"
        @childAdding="handleChildAdding"
      ></ChildComponent>
    </div>
    <h3>Contagem do pai: {{ parentSum }}</h3>
    <button @click="parentSum = 0">Resetar valor do Pai</button>
  </main>
</template>

<style scoped>
main {
  font-size: 26pt;
  display: flex;
  flex-direction: column;
  background-color: rgb(153, 153, 230);
  padding: 5vh;
  border-radius: 30px;
}
.childRow {
  display: flex;
}

button {
  height: 60px;
  font-size: 26pt;
}
</style>
