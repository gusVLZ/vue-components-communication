<script setup lang="ts">
import { ref, watch } from 'vue'

interface InterfaceProps {
  childValue: number
  childName: string
  parentSum: number
}

const childSum = ref<number>(0)

const props = defineProps<InterfaceProps>()

const emit = defineEmits(['childAdding'])

function adding() {
  alert(`Adding do filho ${props.childName} disparou, adicionando ${props.childValue} ao childSum`)
  childSum.value += props.childValue

  alert(`Emitindo childAdding do filho ${props.childName}`)
  emit('childAdding', props.childValue)

  //childAdding(props.value)
}

function reseting() {
  alert(`Reseting do filho ${props.childName} disparou, zerando o valor de childSum`)
  emit('childAdding', childSum.value * -1)
  childSum.value = 0
}

watch(
  () => props.parentSum,
  (n, o) => {
    alert(`Watch do filho ${props.childName} disparou mudando o valor de ${o} para ${n}`)
    if (n == 0) childSum.value = 0
  }
)
</script>

<template>
  <main class="child">
    <h3>O nome do filho é {{ props.childName }}</h3>
    <hr />
    <h5>
      O botão abaixo adiciona <strong>{{ props.childValue }} </strong> a sua própria contagem e
      depois emite ao seu pai o evento
    </h5>
    <button @click="adding">Add {{ props.childValue }}</button>
    <hr />
    <h5>{{ props.childName }} contou até {{ childSum }}</h5>
    <button @click="reseting">Resetar valor do {{ props.childName }}</button>
  </main>
</template>

<style scoped>
.child {
  margin: 10px;
  font-size: 20pt;
  display: flex;
  text-align: center;
  flex-direction: column;
  background-color: rgb(153, 230, 153);
  padding: 5vh;
  border-radius: 30px;
}
button {
  padding: 1em;
  margin: 2em;
}
</style>
