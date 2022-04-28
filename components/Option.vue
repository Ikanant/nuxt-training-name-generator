<template>
  <div class="option-container">
    <h4>{{ option.title }} </h4>
    <!-- <div class="options-buttons">
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
    </div> -->
  </div>
</template>

<script setup lang="ts">
import { Gender, Popularity, Length } from "@/data"
    interface OptionProps {
        option: {
            title:string;
            category: string;
            buttons: Gender[] | Popularity[] | Length[];
        },
        options: {
            gender: Gender;
            popularity: Popularity;
            length: Length;
        }
    }

    const props = defineProps<OptionProps>();
</script>
