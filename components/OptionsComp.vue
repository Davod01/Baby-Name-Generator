<script setup lang="ts">
import { Gender, Length, Popularity,OptionState } from "@/data"

interface optionsProps {
  option: {
    title:string;
    Category: string;
    buttons: Gender[] | Popularity[] | Length[];
  };
  options: OptionState
}
const props = defineProps<optionsProps>()

</script>


<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="option-buttons">
      <button 
      v-for="btn in option.buttons" :key="btn"
      class="option" :class="{'option_active': options[option.Category] === btn}"
      @click="options[option.Category ] = btn"
      >{{btn}}</button>
      <!-- @click="options =  Gender.BOY" -->
    </div>
  </div>
</template>




<style scoped>

.option-container{
  margin-bottom: 2rem;
}
.option{
  background: white;
  outline: 0.15rem solid rgb(249,87,89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27,60,138);
  margin:0.5rem;
  cursor: pointer;
  font-weight: 200;
}
.option-buttons button:first-child{
  border-radius: 1rem 0 0 1rem;
}
.option-buttons button:last-child{
  border-radius:0 1rem 1rem 0;
}

.option_active {
  background-color: rgb(249,87,89);
  color: white;
}
</style>