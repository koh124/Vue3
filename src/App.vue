<!--
Vueではscript, template, styleそれぞれがjs, html, cssに対応している
したがって、各ブロックの中でコメントの記法がそれぞれ言語特有のものになる
js: // または /* */
html: <\!-- --\>
css: /* */
-->

<script setup>
// コンポーネントをデフォルトインポートする
// ↓これはデフォルトインポートじゃない（名前付きインポートと言う）
// import { Hoge } from './components/Hoge.vue'
import HelloWorld from './components/HelloWorld.vue'
import FizzBuzz from './components/FizzBuzz/FizzBuzz.vue';
</script>

<template>
  <!-- 外部リソースの指定の際にサーバールートは/publicになる（コンフィグがあるはず） -->
  <img src="/vite.svg" class="logo" alt="Vite logo" />

  <!-- 相対パスも使える -->
  <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />

  <!-- コンポーネントはHTMLに埋め込む形で使うことになる -->
  <!-- コンポーネントは何度も再利用できる -->

  <!-- 子コンポーネントにpropsを渡すことができる -->
  <!-- propsは子コンポーネントにデータを渡すことができる -->
  <!-- propsで数値を渡したい場合はv-bindを使う -->
  <HelloWorld msg="Vite + Vue" price="1000" />

  <!-- 数値型としてpropsを渡したい場合はv-bindを使う -->
  <HelloWorld msg="Vite + Vue" v-bind:price="1000" />
  <!-- v-bindを省略して:priceのようにすることもできる -->
  <HelloWorld msg="Vite + Vue" :price="1000" />
  <!-- booleanもv-bindで型を合わせることができる -->
  <HelloWorld msg="Vite + Vue" :price="1000" :bool="true" />

  <!-- FizzBuzzアプリ -->
  <FizzBuzz />
</template>
