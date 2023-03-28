<script setup>
// FizzBuzzコンポーネントからpropsを受け取る
const props = defineProps({
  message: String
});
</script>

<template>
  <h2>{{ props.message }}</h2>
</template>
