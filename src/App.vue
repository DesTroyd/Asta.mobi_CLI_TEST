<template>
  <div id="app" class="appWrapper">
    <div class="flex-container">
      <div v-for="(coin, index) in coins" class="coin-block" v-on:click="selectCoin(index)">
        <div style="height: 185px;">
          <img v-bind:src="coin.image">
          <div class=" coin-name">{{coin.name}}</div>
        </div>
        <div class="coin-price">
          <strong style="margin-right: 10px">{{valute[0]}}:</strong> {{coin.price[0]}} <br>
          <strong style="margin-right: 10px">{{valute[1]}}:</strong> {{coin.price[1]}} <br>
          <strong style="margin-right: 10px">{{valute[2]}}:</strong> {{coin.price[2]}}
        </div>
      </div>
    </div>
    <br>
    <div class="selected-coin">Selected coin: {{activeCoin}}</div><br>
    <div class="input-container">
      <span class="input-vol">Volume:</span><input type="text" name="coin-volume" v-model="coinCurrentValue"><br>
    </div>
    <div class="button-select-block">
      <button id="usd" v-on:click="currentValute = valute[0]">USD</button>
      <button id="uah" v-on:click="currentValute = valute[1]">UAH</button>
      <button id="rub" v-on:click="currentValute = valute[2]">RUB</button>
    </div>
    <div class="reult">
      <br><strong>{{coinCurrentValue}}</strong> <strong>{{activeCoin}}</strong> will be <strong>{{amount}}</strong> in <strong>{{currentValute}}</strong>
    </div>
  </div>
</template>

<script>
  const coins = [{
        image: 'https://endotech.io/img/coinicon/BTC.png',
        name: 'BTC',
        price: [6485, 178338, 430454]
      },
      {
        image: 'https://endotech.io/img/coinicon/ETH.png',
        name: 'ETH',
        price: [215.75, 5850, 14319]
      },
      {
        image: 'https://endotech.io/img/coinicon/XRP.png',
        name: 'XRP',
        price: [0.513255, 13.8255, 34.07]
      }
    ],
    valute = ['USD', 'UAH', 'RUB']

  export default {

    data() {
      return {
        valute: valute,
        coinCurrentValue: '',
        coins: coins,
        activeCoin: coins[0].name,
        currentValute: valute[0],

      }
    },

    methods: {
      selectCoin(index) {
        this.activeCoin = coins[index].name
      }
    },

    computed: {
      amount: function() {
        var to = this.currentValute;
        var from = this.activeCoin;
        var final;
        switch (from) {
          case "BTC":
            if (to == "USD") {
              final = this.coinCurrentValue * 6800;
            }
            if (to == "UAH") {
              final = this.coinCurrentValue * 150000;
            }
            if (to == "RUB") {
              final = this.coinCurrentValue * 340000;
            }
            break;
          case "ETH":
            if (to == "USD") {
              final = this.coinCurrentValue * 250;
            }
            if (to == "UAH") {
              final = this.coinCurrentValue * 7400;
            }
            if (to == "RUB") {
              final = this.coinCurrentValue * 16000;
            }
            break;
          case "XRP":
            if (to == "USD") {
              final = this.coinCurrentValue * 0.2500;
            }
            if (to == "UAH") {
              final = this.coinCurrentValue * 7.0231;
            }
            if (to == "RUB") {
              final = this.coinCurrentValue * 17.228;
            }
            break;
        }
        return final;
      }
    },
  }
</script>

<style>
  body {
    font-size: 32px;
    margin: 0;
    padding-left: 30px;
    background-color: #06162e;
  }

  .appWrapper {

    align-items: center;
    align-content: space-between;
  }

  .coin-block {
    display: inline-flex;
    background-color: #102f52;
    margin: 20px;
    padding: 20px 20px 30px 20px;

  }

  .coin-block:hover {
    background-color: #153d6a;
  }

  .coin-block:active {
    background-color: #113155;
  }

  .coin-name {
    color: #86c551
  }

  .coin-price {
    color: #5594dd;
    margin-left: 20px;
  }

  .selected-coin {
    text-align: center;
    color: #5594dd;
  }

  .flex-container {
    display: flex;
    justify-content: center;
  }

  .input-container {
    text-align: center;
    color: #86c551;
    margin: 0px auto;
  }

  .button-select-block {
    text-align: center;
  }

  .reult {
    color: #86c551;
    text-align: center;
  }

  input {
    background-color: #06162e;
    border: 1px solid #5594dd;
    border-radius: 3px;
    width: 400px;
    height: 25px;
    margin-left: 5px;
    margin-right: 90px;
    color: #5594dd;
    padding-left: 10px;
  }

  input[type=text]:focus {
    outline: none
  }

  .input-vol {
    font-size: 24px;
  }

  button {
    background-color: #102f52;
    color: #86c551;
    border: 2px solid #102f52;
    height: 30px;
    margin-left: 5px;
  }

  button:focus {
    outline: none;
    background-color: #86c551;
    color: #102f52;
    border: 2px solid #86c551;
  }
</style>