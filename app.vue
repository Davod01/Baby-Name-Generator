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
    </div>
    
  </div>
</template>


<script setup lang="ts">
enum Gender {
  GIRL= "Girl",
  BOY= "Boy",
  UNISEX= "Unisex"
}
enum Popularity {
  TRENDY= "Trendy",
  UNIQUE= "Unique"
}
enum Length {
  SHORT = "Short",
  ALL = "All",
  LONG = "Long"
}

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
</style>