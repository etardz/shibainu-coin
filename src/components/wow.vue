<template>
  <section class="wow">
    <div class="progressBarContainer">
      <img class="centImage" :src="centImage">
      <div class="progressBarLeft" :style="`width: ${shibainuPrice * 10000}%`">
        <div class="wowContainer" id="wowContainer">
          <img id="shibainuImage" class="shibainuImage" :src="shibainuImage" />
          <main :style="`color: ${color}`">{{ String(shibainuPrice).padEnd(10, '0') }}</main>
        </div>
      </div>
      <div class="progressBarRight" :style="`width: ${(1 - shibainuPrice * 100) * 100}%`"></div>
    </div>
  </section>
</template>
<script>
import shibainuImage from '/shibainu.png';
import centImage from '/cent.jpg';

const greenColor = 'rgba(34, 168, 30, 0.7)';
const redColor = 'rgba(253, 4, 4, 0.7)';

export default {
  props: {
    shibainuPrice: {
      type: Number,
      required: true
    },
    ticker: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      color: 'black',
      previousPrice: 0,
      shibainuImage,
      centImage
    }
  },
  methods: {
    generateWow(value) {
      const allWowText = document.getElementsByName('wowText');
      const len = allWowText.length;
      // remove previous text
      for (let i = 0; i < len; i++) {
        allWowText[i].parentNode.removeChild(allWowText[i]);
      }
      const shibainuImage = document.getElementById("shibainuImage");
      const wow = document.createElement("div");
      wow.setAttribute('name', 'wowText');
      wow.classList.add('wowText');
      if (value === 1) {  // price increse
        wow.classList.add('increaseAnimation');
        shibainuImage.classList.add("mirror");
      } else if (value === -1) {  // price decrese
        wow.classList.add('decreaseAnimation');
        shibainuImage.classList.remove("mirror");
      } else {  // price not change
        wow.classList.add('equalAnimation');
        shibainuImage.classList.remove("mirror");
      }
      const wowText = document.createTextNode("wow");
      wow.appendChild(wowText);
      
      const wowContainer = document.getElementById('wowContainer');
      wowContainer.appendChild(wow);  // show the wow text
    }
  },
  watch: {
    ticker() {
      if (this.shibainuPrice > this.previousPrice) {
        this.color = greenColor;
        this.generateWow(1);
      } else if (this.shibainuPrice === this.previousPrice) {
        this.color = 'black';
        this.generateWow(0);
      } else {
        this.color = redColor;
        this.generateWow(-1);
      }
      this.previousPrice = this.shibainuPrice;
    }
  }
}
</script>
