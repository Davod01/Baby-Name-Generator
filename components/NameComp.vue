<script setup lang="ts">
const props = defineProps<{
  selectedNames: string[]
}>()

</script>

<template>
  <div class="cards-container">
    <div v-for="(Name, index) in selectedNames" :index="index" :key="index" class="card">
      <h4>{{ Name }}</h4>
      <p @click="$emit('removeName', index)">x</p>
    </div>
  </div>
</template>

<style scoped>
.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}

.card{
  background-color: rgb(27,60,138);
  color: white;
  width: 28%;
  border-radius: 1rem;
  padding: 0.1rem;
  margin: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}

.card p {
  position: absolute;
  top: -28%;
  left: 91%;
  cursor: pointer;
  color: rgba(255,255,255,0.178);
}
</style>