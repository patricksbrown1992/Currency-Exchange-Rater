

<template>
  <div id="app">
 
    <p>Original Currency</p>
    <input id='originalCurrency' v-model="originalCurrency">
    <p>Desired Currency</p>
    <input v-model="endCurrency">
    <p>Amount</p>
    <input v-model='amt'>
    <button v-on:click = "getData">add</button>
    {{res[res.length-1]}}
  </div>
</template>

<script>


import jquery from 'jquery'
export default {
  name: 'App',
 
  data(){
    return{
      originalCurrency: '',
      endCurrency: '',
      date: new Date().toJSON().slice(0,10),
      res: [],
      amt: 0

    }
  },
  methods: {
    getData: function(){
      const settings = {"async": true,"crossDomain": true, "url": `https://currency-converter5.p.rapidapi.com/currency/convert?format=json&from=${this.originalCurrency}&to=${this.endCurrency}&amount=${this.amt}`,"method": "GET","headers": {"x-rapidapi-host": "currency-converter5.p.rapidapi.com", "x-rapidapi-key": "432cb85f3emshd2e70eeb3556d3bp144a56jsn06cbcafb135e"}}

      jquery.ajax(settings).then(res => {this.res.push(Object.values(res.rates)[0].rate_for_amount)}) 


      
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
input{
  outline: none;
  margin-top: 5px;
  margin-bottom: 35px;
}

</style>
