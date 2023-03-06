<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options andd click the "Find Names" buttom below</p>
    <div class="options-container">
      <div class="option-container">
        <h4>1) Choose a gender</h4>
        <div class="option-buttons">
          <button
          class="option"
          :class="{'option_active': options.Gender === Gender.GIRL}"
          @click="options.Gender = Gender.GIRL"
          >Boy</button>
          <button
          class="option"
          :class="{'option_active': options.Gender === Gender.UNISEX}"
          @click="options.Gender =  Gender.UNISEX"
          >Unisex</button>
          <button
          class="option"
          :class="{option_active: options.Gender === Gender.BOY}"
          @click="options.Gender =  Gender.BOY"
          >Girl</button>
        </div>
      </div>
      <div class="option-container">
        <h4>2) Choose the name's popularity</h4>
        <div class="option-buttons">
          <button
          class="option"
          :class="{option_active: options.Popularity == Popularity.TRENDY}"
          @click="options.Popularity =  Popularity.TRENDY"
          >Trendy</button>
          <button
          class="option"
          :class="{option_active: options.Popularity == Popularity.UNIQUE}"
          @click="options.Popularity =  Popularity.UNIQUE"
          >Unique</button>
        </div>
      </div>
      <div class="option-container">
        <h4>3) Choose name length</h4>
        <div class="option-buttons">
          <button
          class="option"
          :class="{option_active: options.Length == Length.LONG}"
          @click="options.Length =  Length.LONG"
          >Long</button>
          <button
          class="option"
          :class="{option_active: options.Length == Length.ALL}"
          @click="options.Length =  Length.ALL"
          >All</button>
          <button
          class="option"
          :class="{option_active: options.Length == Length.SHORT}"
          @click="options.Length =  Length.SHORT"
          >Short</button>
        </div>
      </div>
      <button class="primary" @click="computedSelectedName">Find Names</button>
      <div>
        {{ selectedNames }}
      </div>
    </div>
    
  </div>
</template>


<script setup lang="ts">
import {Gender,Popularity,Length,names} from "@/data"

interface OptionState {
  Gender: Gender;
  Popularity: Popularity;
  Length: Length;
}
const options = reactive<OptionState>({
  Gender: Gender.GIRL,
  Popularity: Popularity.UNIQUE,
  Length: Length.ALL,
})

const selectedNames = ref<string[]>([])

const computedSelectedName = () => {
  const filtredName = names.filter(name => name.gender === options.Gender)
    .filter(name => name.popularity === options.Popularity)
    .filter(name => {
      if (options.Length === Length.ALL) return true
      else return name.length === options.Length
    })
  selectedNames.value = filtredName.map(name => name.name)
}

</script>



<style scoped>
.container{
  font-family: Arial, Helvetica, sans-serif;
  color:rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}
h1{
  font-size: 3rem;
}

.options-container{
  background-color: rgb(255,238,236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}
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
.option-container button:first-child{
  border-radius: 1rem 0 0 1rem;
}
.option-container button:last-child{
  border-radius:0 1rem 1rem 0;
}

.option_active {
  background-color: rgb(249,87,89);
  color: white;
}

.primary {
  background-color: rgb(249,87,89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}
</style>