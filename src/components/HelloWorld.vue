<script setup>
/*
・script setup
コンポーネントのセットアップ関数
コンポーネントがwebページにマウント（描画）される前に前処理で実行される
コンポーネントはインスタンス単位で扱われる

scriptブロックは基本的に1ファイルに1つしか定義できない
scriptとsetupは互いに1つずつだけ共存が可能
- <script> OK
- <script setup> OK
- <script> + <script> NG
- <script setup> + <script setup> NG

・コンポーネント
コンポーネントはVueプロジェクトを構成する一つ一つのレゴブロックのようなもの
Vueアプリケーションはコンポーネント単位で構成され、
これらを組み合わせて最終的に一つのアプリケーションとして統合される
*/
import { ref } from 'vue';

// 親コンポーネントからpropsを受け取るにはdefinePropsを使う
// propsの受け取り方には様々な方法がある
// defineProps({
//   msg: String,
// })
// defineProps(['msg']);
const { msg, price, hoge } = defineProps({
  msg: {
    type: String,
    required: true // 親コンポーネントがpropsを渡すことを必須にする
  },
  price: {
    // type: Numberによる型情報は渡されるpropsが数値型であることを保証するものではない
    // <HelloWorld price="1000" />のように渡されても、
    // 子コンポーネントでは文字列として解釈してしまう
    // 親コンポーネントでv-bindを設定することで、型情報が正しく反映される
    // ↓コンソールに表示されるwarning
    // [Vue warn]: Invalid prop: type check failed for prop "price".
    // Expected Number with value 1000, got String with value "1000".
    // at <HelloWorld msg="Vite + Vue" price="1000" >
    // at <App>
    type: Number,
  },
  bool: Boolean,
  hoge: {
    type: String,
    default: '親コンポーネントからpropsが渡されなかったときのデフォルトの値'
  }
})

// refはreactで言うところのstate
// 値をブラウザ上で保持することができる
// 初期値を0にセットする
const count = ref(0);

console.log('script setup');
</script>

<script>
/*
scriptはsetupよりも先に実行される
ネットワークからダウンロードできたときに実行される（？）と思われる
*/

// scriptはsetupよりも後に定義されているが、
// setupよりも先に出力される
console.log('script')
</script>

<template>
  <!-- Vueではtemplateも1ファイルにつき1つしか定義できない -->
  <h1>{{ msg }}</h1>
  <h2>{{ price + 100 }}</h2>
  <h2>{{ hoge }}</h2>
  <h2 v-if="!bool">{{ 'bool props has passed' }}</h2>

  <!--
  ・Vueではon{EventName}のonが@に置き換わる
  ・@event属性の値はjavascriptの式として解釈される
  ・引数は$argumentで受け取り、scriptブロックで定義された変数は接頭辞なしでそのまま値を参照できる
  ・{{ }}でscriptの変数を展開できる
  -->
  <button class="border red" type="button" @click="count++">count is {{ count }}</button>
</template>

<style scoped>
/*
  scopedはCSSがこのコンポーネントにしか適用されないことを宣言する
  つまり、ローカルスコープを作る
*/
.border {
  border: 1px solid skyblue;
}
</style>

<style scoped>
/*
  styleは1つのファイルに複数定義できる
*/
.red {
  color: red;
}
</style>
