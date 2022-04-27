<template>
  <div class="container">
    <h1>Name Generator</h1>

    <p>Please select your options and click the "FIND NAMES" button bellow</p>

    <div class="options-container">
      <div class="option-container">
        <h4>1) Choose a gender:</h4>
        <div class="options-buttons">
          <button
            class="option option-left"
            :class="options.gender === Gender.BOY && 'option-active'"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="option"
            :class="options.gender === Gender.UNISEX && 'option-active'"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
            class="option option-right"
            :class="options.gender === Gender.GIRL && 'option-active'"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>2) Choose name's popularity:</h4>
        <div class="options-buttons">
          <button
            class="option option-left"
            :class="options.popularity === Popularity.TRENDY && 'option-active'"
            @click="options.popularity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
            class="option option-right"
            :class="options.popularity === Popularity.UNIQUE && 'option-active'"
            @click="options.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>3) Choose the name's length:</h4>
        <div class="options-buttons">
          <button
            class="option option-left"
            :class="options.length === Length.LONG && 'option-active'"
            @click="options.length = Length.LONG"
          >
            Long
          </button>
          <button
            class="option"
            :class="options.length === Length.ALL && 'option-active'"
            @click="options.length = Length.ALL"
          >
            All
          </button>
          <button
            class="option option-right"
            :class="options.length === Length.SHORT && 'option-active'"
            @click="options.length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    {{ activeNames }}
  </div>
</template>

// Use setup flag to start getting started with the composition api.
// Lang is a simple way to we start using typescript in our script.
<script setup lang="ts">
import {Gender, Popularity, Length, names} from "@/data";

// Create interface for options object
interface OptionState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

// NOTICE: Did NOT import reactive. NUXT is going to take care of the auto-importation
// NOTICE x2: With SETUP flag in the script we do NOT need to export anything in order to use it in template.
//            We can now use options int he html section of this code.
// NOTICE x3: I can use the colon to specify options type OR I can use the <> after the reactive api tool
const options: OptionState = reactive<OptionState>({
  gender: Gender.GIRL,
  popularity: Popularity.TRENDY,
  length: Length.ALL,
});


// NOTICE: Instead of being reactive, just set it to ref since this should be a simple array
let activeNames = ref<string[]>([])

const computeSelectedNames = () => {
  var filteredNames = names.filter(f => {
    return f.gender === options.gender && f.popularity === options.popularity;
  }).filter(l => {
    if (options.length === Length.ALL) return true;
    return l.length === options.length;
  });

  activeNames.value = filteredNames.map(m => m.name);
}
</script>


<style scoped>
.container {
  font-family: Arial, Arial, Helvetica, sans-serif;
  color: teal;
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3rem;
}

.options-container {
  background-color: aquamarine;
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

.option-container {
  margin-bottom: 2rem;
}

.option {
  background-color: white;
  outline: 0.15rem solid teal;
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: blue;
  cursor: pointer;
  font-weight: 200;
}

.option-left {
  border-radius: 1rem 0 0 1rem;
}

.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-active {
  background-color:teal;
  color: white;
}

.primary {
  background-color: teal;
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
}
</style>