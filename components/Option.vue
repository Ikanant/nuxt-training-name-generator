<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="options-buttons">
      <button
        class="option"
        v-for="(button, index) in option.buttons"
        :key="button"
        :class="computeButtonClasses(button, index)"
        @click="options[option.category] = button"
      >
        {{ button }}
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Gender, Popularity, Length } from "@/data";
interface OptionProps {
  option: {
    title: string;
    category: string;
    buttons: Gender[] | Popularity[] | Length[];
  };
  options: {
    gender: Gender;
    popularity: Popularity;
    length: Length;
  };
}

const props = defineProps<OptionProps>();

const computeButtonClasses = (button, index) => {
    const classNames:string[] = [];
    if (props.options[props.option.category] === button) {
        classNames.push("option-active");
    }

    if (index == 0) {
        classNames.push("option-left");
    }
    else if (index === props.option.buttons.length-1) {
        classNames.push("option-right");
    }

    return classNames.join(" ");
}
</script>

<style scoped>
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
  background-color: teal;
  color: white;
}
</style>
