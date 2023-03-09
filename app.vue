<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options andd click the "Find Names" buttom below</p>
    <div class="options-container">
      <OptionsComp v-for="option in optionsArray" :key="option.title"
      class="option-container" :option="option" :options="options" />
      <button class="primary" @click="computedSelectedName">Find Names</button>
      <NameComp :selectedNames="selectedNames" @removeName="removeName" />
    </div>
  </div>
</template>


<script setup lang="ts">
import {Gender,Popularity,Length,names,OptionState} from "@/data"

const options = reactive<OptionState>({
  Gender: Gender.BOY,
  Popularity: Popularity.TRENDY,
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

const optionsArray = [
  {
    title:"1) Choose a gender",
    Category: "Gender",
    buttons:[Gender.GIRL,Gender.UNISEX,Gender.BOY]
  },
  {
    title:"2) Choose the name's popularity",
    Category: "Popularity",
    buttons:[Popularity.TRENDY,Popularity.UNIQUE]
  },
  {
    title:"3) Choose name length",
    Category: "Length",
    buttons:[Length.ALL,Length.LONG,Length.SHORT]
  },
]

const removeName = (index: number) =>{
  selectedNames.value.splice(index, 1)
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