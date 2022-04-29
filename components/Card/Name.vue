<template>
  <div class="card">
    <label>{{ name }}</label>
    <p @click="emitRemoveNameEvent" >X</p>
  </div>
</template>

<script setup lang="ts">
interface NameProps {
  name: string;
  index: number;
}

const props = defineProps<NameProps>();
const emit = defineEmits(["removeNameEvent"]);

const  emitRemoveNameEvent = () => {
    emit("removeNameEvent", props.index);
}
</script>

<style scoped>
.card {
  background-color: teal;
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}

.card p {
  position: absolute;
  top: -20%;
  left: 92.5%;
  width: 10px;
  cursor: pointer;
  color: white;
}
</style>
