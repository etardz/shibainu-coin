<template>
  <section class="app">
    <Message />
    <Wow :shibainuPrice="shibainuPrice" :ticker="ticker" />
  </section>
</template>
<script>
import axios from 'axios';
import Message from './components/message.vue';
import Wow from './components/wow.vue';

export default {
  data() {
    return {
      shibainuPrice: 0,
      ticker: 0  // sysbol for update price
    }
  },
  components: { Wow, Message },
  async mounted() {
    const url = 'https://api.binance.com';
    const symbol = 'SHIBUSDT';
    const res = await axios.get(`${url}/api/v3/ticker/price?symbol=${symbol}`);
    this.shibainuPrice = Number(res.data.price);
    this.ticker += 1;
    if (!!window) {
      window.getPrice = setInterval(async () => {
        const res = await axios.get(`${url}/api/v3/ticker/price?symbol=${symbol}`);
        this.shibainuPrice = Number(res.data.price);
        this.ticker += 1;
        document.title = `[$${this.shibainuPrice}] Shiba Inu To 1 Penny!`;
      }, 1000);
    }
  },
  beforeUnmount() {
    if (!!window) {
      clearInterval(window.getPrice);
    }
  }
    
}
</script>
