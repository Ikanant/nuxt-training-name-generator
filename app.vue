<template>
  <div class="container">
    <h1>Name Generator</h1>

    <p>Please select your options and click the "FIND NAMES" button bellow</p>

    <div class="options-container">
      <!-- Because we are using NUXT, we do NOT need to import the Option component -->
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />

      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    <div class="card-container">
      <!-- Thing to not is that the Name component is inside a CARD folder. So here, when using NUXT we need to reference the name as:
      <DirectoryName><ComponentName> -->
      <CardName
        v-for="(name, index) in activeNames"
        :key="name"
        :name="name"
        :index="index"
        @removeNameEvent="removeNameFunction(index)"
      />
    </div>
  </div>
</template>

// Use setup flag to start getting started with the composition api. // Lang is
a simple way to we start using typescript in our script.
<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data";

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

const optionsArray = [
  {
    title: "1) Choose a gender",
    category: "gender",
    buttons: [Gender.GIRL, Gender.BOY, Gender.UNISEX],
  },
  {
    title: "2) Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose the name's length",
    category: "length",
    buttons: [Length.SHORT, Length.LONG, Length.ALL],
  },
];

// NOTICE: Instead of being reactive, just set it to ref since this should be a simple array
let activeNames = ref<string[]>([]);

const computeSelectedNames = () => {
  var filteredNames = names
    .filter((f) => {
      return f.gender === options.gender && f.popularity === options.popularity;
    })
    .filter((l) => {
      if (options.length === Length.ALL) return true;
      return l.length === options.length;
    });

  activeNames.value = filteredNames.map((m) => m.name);
};

const removeNameFunction = (index: number) => {
  activeNames.value.splice(index, 1);
};
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

.primary {
  background-color: teal;
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.card-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}
</style>
