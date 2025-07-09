<template>
  <ul class="list">
    <li @click="setCrypto('BTC')" :class="cryptoNow === 'BTC' ? 'active': ''">BITCOIN</li>
    <li @click="setCrypto('ETH')" :class="cryptoNow === 'ETH' ? 'active': ''">ETH</li>
    <li @click="setCrypto('USDT')" :class="cryptoNow === 'USDT' ? 'active': ''">USDT</li>
  </ul>
</template>

<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      required: true
    },
    cryptoNow: {
      type: String,
      required: true
    }
  },
};
</script>

<style scoped>
.list {
  text-align: center;
  list-style: none;
  width: 200px;
  padding: 0;
  border-radius: 3px;
  border: 3px solid #000;
  margin: 10px;
}
li {
  display: block;
  background: #1A032D;
  color: #fff;
  padding: 20px 0;
}
li:hover{
  cursor: pointer;
  background: #24043e;
}
.active{
  background: #24043e;
}
</style>
