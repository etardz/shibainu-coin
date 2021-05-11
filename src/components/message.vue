<template>
  <section class="message">
    <header>{{ msg.title }}</header>
    <main>{{ msg.main }}</main>
  </section>
</template>
<script>
export default {
  data() {
    return {
      msg: {
        title: 'Shiba Inu Coin Sure To Be One Penny',
        main: 'Be Diamond💎 Hand✋ Instead Of Papper📄 Hand👋'
      }
    }
  }
}
</script>