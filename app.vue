<template>
  <div class="container">
    <h1>Name Generator</h1>

    <p>Please select your options and click the "FIND NAMES" button bellow</p>

    <div class="options-container">
      <div class="option-container">
        <h4>1) Choose a gender:</h4>
        <div class="options-buttons">
          <button class="option option-left">Boy</button>
          <button class="option">Unisex</button>
          <button class="option option-right">Girl</button>
        </div>
      </div>
      <div class="option-container">
        <h4>2) Choose name's popularity:</h4>
        <div class="options-buttons">
          <button class="option option-left">Trendy</button>
          <button class="option option-right">Unique</button>
        </div>
      </div>
      <div class="option-container">
        <h4>3) Choose the name's length:</h4>
        <div class="options-buttons">
          <button class="option option-left">Long</button>
          <button class="option">All</button>
          <button class="option option-right">Short</button>
        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>
.container {
  font-family: Arial, Arial, Helvetica, sans-serif;
  color:rgb(27,60,138);
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
  outline: 0.15rem solid red;
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
</style>