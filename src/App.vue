<template>
  <h1>CRYPTO</h1>
  <Input :changeAmount="changeAmount" :convert="convert" :favourite="favourite"/>
  <p v-if="error != ''">{{ error }}</p>
  <p class="result" v-if="result != ''">{{ resultIs }}</p>
  <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs" :deleteFav="deleteFav"/>
  <div class="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond":cryptoNow="cryptoSecond"/>
  </div>
</template>

<script>
import CryptoConvert from 'crypto-convert';
import Input from './components/input.vue';
import Selector from './components/Selector.vue';
import Favourite from './components/Favourite.vue';

const convert = new CryptoConvert()

export default {
  components: { Input, Selector, Favourite },
  data() {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0,
      favs: []
    };
  },
  computed: {
    resultIs(){
      return `Your result is: ${this.result}` 
    }
  },
  methods: {
    changeAmount(val) {
      this.amount = val;
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },  
    async convert(){
      if(this.amount <= 0){
        this.error = 'The amount is zero';
        this.result = ''
      } else if(this.cryptoFirst === this.cryptoSecond && this.amount > 0) {
        this.error = 'Currencies are same';
        this.result = ''
      } else if(this.cryptoFirst === '' || this.cryptoSecond === '') {
        this.error = 'Choose all currencies';
        this.result = ''
      } else {
        this.error = ''
      }
      await convert.ready()
      if(this.cryptoFirst === 'BTC' && this.cryptoSecond === 'ETH'){
        this.result = convert.BTC.ETH(this.amount);
      } else if(this.cryptoFirst === 'BTC' && this.cryptoSecond === 'USDT'){
        this.result = convert.BTC.USDT(this.amount);
      } else if(this.cryptoFirst === 'ETH' && this.cryptoSecond === 'BTC'){
        this.result = convert.ETH.BTC(this.amount);
      } else if(this.cryptoFirst === 'ETH' && this.cryptoSecond === 'USDT'){
        this.result = convert.ETH.USDT(this.amount);
      } else if(this.cryptoFirst === 'USDT' && this.cryptoSecond === 'BTC'){
        this.result = convert.USDT.BTC(this.amount);
      } else if(this.cryptoFirst === 'USDT' && this.cryptoSecond === 'ETH'){
        this.result = convert.USDT.ETH(this.amount);
      }
    },
    favourite(){
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond
      })
    },
    getFromFavs(index) {
      this.cryptoFirst = this.favs[index].from;
      this.cryptoSecond = this.favs[index].to;
    },
    deleteFav(index){
      this.favs.splice(index, 1)
    }
  }
};
</script>
<style scoped>
.selectors {
  display: flex;
  justify-content: center;
}
p{
  color: rgb(192, 35, 35);
}
.result{
  color: #fafafa;
}
</style>
