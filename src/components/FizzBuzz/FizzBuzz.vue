<script setup>
import Fizz from './Fizz.vue';
import Buzz from './Buzz.vue';
import { ref, reactive } from 'vue';

// vueではstate変数のことを"reactivityを持つ"と呼んでいる
// ref, reactive関数を使って状態を保持することができる
const count = ref(0);
const state = reactive({
  count: 0
});

// refオブジェクトはvalueを更新することで再レンダリングがスケジュールされる
const handleClick = (e) => {
  count.value++;
}

// reactiveオブジェクトは変数名に直接アクセスして更新する
const addReactive = (e) => {
  state.count++
}
</script>

<script>
const fizzBuzzCount = ref(0);
</script>

<template>
  <h2>Ref {{ count }}</h2>
  <h2>Reactive {{ state.count }}</h2>
  <div class="flex">
    <!-- templateのrefオブジェクトではvalueにアクセスしなくても更新できる -->
    <button @click="$event => count++">Ref +1</button>
    <button @click="handleClick">Ref +1</button>

    <!-- reactiveオブジェクトで更新するにはオブジェクトから変数名にアクセスする -->
    <button @click="addReactive">Reactive +1</button>
    <button @click="$event => state.count++">Reactive +1</button>
  </div>

  <h2>↓FizzBuzzアプリ</h2>
  <p>fizzBuzzCount value: {{ fizzBuzzCount }}</p>
  <button @click="$event => fizzBuzzCount++">FizzBuzz + 1</button>

  <!-- Fizz, Buzzコンポーネントにはpropsでmessageを渡している -->
  <h2 v-if="fizzBuzzCount % 15 === 0">FizzBuzz!</h2>
  <Fizz v-else-if="fizzBuzzCount % 3 === 0" message="Fizz" />
  <Buzz v-else-if="fizzBuzzCount % 5 === 0" message="Buzz" />
  <h2 v-else>{{ fizzBuzzCount }}</h2>
</template>

<style scoped>
.flex {
  display: flex;
}
</style>
