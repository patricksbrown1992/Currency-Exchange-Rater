

<template>
  <div id="app">
 
    <p>Original Currency</p>
    <select v-model='originalCurrency'>

      <option value="AUD">AUD</option>
      <option value="BGN">BGN</option>
      <option value="BRL">BRL</option>
      <option value="CAD">CAD</option>
      <option value="CHF">CHF</option>
      <option value="CNY">CNY</option>
      <option value="CZK">CZK</option>
      <option value="DEK">DKK</option>
      <option value="EUR">EUR</option>
      <option value="GBP">GBP</option>
      <option value="HKD">HKD</option>
      <option value="HRK">HRK</option>
      <option value="HUF">HUF</option>
      <option value="IDR">IDR</option>
      <option value="ILS">ILS</option>
      <option value="INR">INR</option>
      <option value="ISK">ISK</option>
      <option value="JPY">JPY</option>
      <option value="KRW">KRW</option>
      <option value="MXN">MXN</option>
      <option value="MYR">MYR</option>
      <option value="NOK">NOK</option>
      <option value="NZD">NZD</option>
      <option value="PHP">PHP</option>
      <option value="PLN">PLN</option>
      <option value="RON">RON</option>
      <option value="RUB">RUB</option>
      <option value="SEK">SEK</option>
      <option value="SGD">SGD</option>
      <option value="THB">THB</option>
      <option value="TRY">TRY</option>
      <option value="USD">USD</option>
      <option value="ZAR">ZAR</option>
    </select>
    
    <p>Desired Currency</p>
  
    <select v-model='endCurrency'>

      <option value="AUD">AUD</option>
      <option value="BGN">BGN</option>
      <option value="BRL">BRL</option>
      <option value="CAD">CAD</option>
      <option value="CHF">CHF</option>
      <option value="CNY">CNY</option>
      <option value="CZK">CZK</option>
      <option value="DKK">DKK</option>
      <option value="EUR">EUR</option>
      <option value="GBP">GBP</option>
      <option value="HKD">HKD</option>
      <option value="HRK">HRK</option>
      <option value="HUF">HUF</option>
      <option value="IDR">IDR</option>
      <option value="ILS">ILS</option>
      <option value="INR">INR</option>
      <option value="ISK">ISK</option>
      <option value="JPY">JPY</option>
      <option value="KRW">KRW</option>
      <option value="MXN">MXN</option>
      <option value="MYR">MYR</option>
      <option value="NOK">NOK</option>
      <option value="NZD">NZD</option>
      <option value="PHP">PHP</option>
      <option value="PLN">PLN</option>
      <option value="RON">RON</option>
      <option value="RUB">RUB</option>
      <option value="SEK">SEK</option>
      <option value="SGD">SGD</option>
      <option value="THB">THB</option>
      <option value="TRY">TRY</option>
      <option value="USD">USD</option>
      <option value="ZAR">ZAR</option>
    </select>
    <p>Amount</p>
    <input v-model='amt'>
    <button v-on:click = "getData">add</button>
    {{res}}
    {{err}}


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
      res: null,
      amt: 0,
      err: null,

    }
  },
  methods: {
    getData: function(){

    if (!isNaN(this.amt)) {
      this.err = null
      this.res = null
      const settings = {"async": true,"crossDomain": true, "url": `https://currency-converter5.p.rapidapi.com/currency/convert?format=json&from=${this.originalCurrency}&to=${this.endCurrency}&amount=${this.amt}`,"method": "GET","headers": {"x-rapidapi-host": "currency-converter5.p.rapidapi.com", "x-rapidapi-key": "432cb85f3emshd2e70eeb3556d3bp144a56jsn06cbcafb135e"}}
  
      jquery.ajax(settings).then(res => {this.res = Object.values(res.rates)[0].rate_for_amount}).catch(err => this.err = err.responseJSON.error.message)
        
      } else {
        this.res = null
        this.err = 'Please enter a valid number'
      }

      
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
select{
  outline: none;
}
button{
  margin-bottom: 10px;
}
</style>
