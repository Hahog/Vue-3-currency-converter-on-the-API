
<template>
  <section>
    <article>
      <h1>Конвертор валют</h1>
      <p>Конвертировать в {{ src ? src  : 'валюту' }}</p>
    </article>
    <article>
      <input type="number" placeholder="Сумма"  v-model="valut">
      <button v-show="valut" @click="getCurs()">Конвертировать</button>
    </article>
    <article>
      <select v-model="src">
        <option v-for="(val, key) in curs" :key="key"> {{val.CharCode}}</option>
      </select>
      <h1 v-show="res">{{ src + ": " + res.toFixed(2) }}</h1>
    </article>
  </section>
</template>

<script>
  import axios from 'axios'
  export default {
    data() {
      return {
        valut: null,
        src: "",
        curs: 111,
        res: 0
      }
    },
    beforeMount() {
      axios.get("https://www.cbr-xml-daily.ru/daily_json.js").then((res) => {this.curs = res.data.Valute})
    },
    methods: {
      getCurs() {
        this.res = this.valut / (this.curs[this.src].Value.toFixed(2) / this.curs[this.src].Nominal)
      }
    }
  }
</script>

<style scoped>

</style>
