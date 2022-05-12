<script setup>
import CryptoSection from '@/components/Crypto-section.vue'
import StockSection from '@/components/Stock-section.vue'
import FooterArea from '@/components/UI/Footer-area.vue'
import { ref } from 'vue'

const component = ref(StockSection)
const stockButtonStyle = ref('stocks-button')
const cryptoButtonStyle = ref(null)

function chooseComponent(cmp) {
  component.value = cmp
  if (component.value !== StockSection) {
    document.body.classList.add('crypto-background')
    stockButtonStyle.value = null
    cryptoButtonStyle.value = 'crypto-button'
  } else {
    document.body.classList.remove('crypto-background')
    stockButtonStyle.value = 'stocks-button'
    cryptoButtonStyle.value = null
  }
}
</script>

<template>
  <div class="content-container">
    <div class="hero-container">
      <h1 v-if="component === 'StockSection'" class="stock-header">Vue Stock App</h1>
      <h1 v-else class="crypto-header">Vue Crypto App</h1>
      <!-- NAVIGATION AREA TO SWTICH BETWEEN COMPONENTS -->
      <div class="tabs">
        <button :class="stockButtonStyle" class="button stock-default" @click="chooseComponent(StockSection)">
          Stocks
        </button>
        <button :class="cryptoButtonStyle" class="button crypto-default" @click="chooseComponent(CryptoSection)">
          Crypto
        </button>
      </div>
      <keep-alive>
        <component :is="component"></component>
      </keep-alive>
      <img v-if="component === 'StockSection'" class="crypto-logo" src="../src/images/stocks-logo.png" alt="" />
      <img v-else class="crypto-logo" src="../src/images/crypto-logo.png" alt="" />
    </div>
  </div>
  <FooterArea />
</template>

<style>
/* GLOBAL STYLES */
* {
  font-family: 'Nunito', sans-serif;
}

.crypto-background {
  background: linear-gradient(to bottom, #080808, rgb(0, 20, 42));
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}

body {
  background: linear-gradient(to bottom, #080808, #001402);
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  margin: 0;
}

.content-container {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 90vh;
  margin-bottom: 5em;
}

.stock-header {
  text-align: center;
  font-size: 82px;
  font-family: 'Nunito', sans-serif;
  font-style: italic;
  background-image: linear-gradient(to right, #002d05 10%, #52e24b 90%);
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

.crypto-header {
  text-align: center;
  font-size: 82px;
  font-family: 'Nunito', sans-serif;
  font-style: italic;
  background-image: linear-gradient(to right, #00102d 10%, #1097f7 90%);
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* NAV AREA */

.tabs {
  width: 500px;
  margin: 0 auto 2.5em auto;

  text-align: center;
}

.button {
  height: 2.5em;
  width: 175px;
  margin: 0.5em;

  background-color: #004f6b47;
  color: #ffffffab;
  font-size: 1.2em;
  font-family: 'Nunito', sans-serif;

  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
  border: none;
  cursor: pointer;
  transition: 0.2s ease;
}

.stocks-button {
  margin-right: 0.5em;
  border-bottom: 2px solid;
  border-image: linear-gradient(to right, #002f09, #52e24b) 1;
}

.crypto-button:hover {
  background-color: #004f6b8f;
}

.stocks-button:hover {
  background-color: #006b248f;
}

.crypto-button {
  border-bottom: 2px solid;
  border-image: linear-gradient(to right, #03254e, #1097f7) 1;
  border-bottom-right-radius: 10px;

  transition: 0.2s ease;
}

.crypto-button:active {
  background-color: #03254e;
  color: #e7f0ff;
}

.crypto-default:hover {
  border-bottom: 2px solid;
  border-image: linear-gradient(to right, #03254e, #1097f7) 1;
}

.stock-default:hover {
  border-bottom: 2px solid;
  border-image: linear-gradient(to right, #002f09, #52e24b) 1;
}

.stocks-logo,
.crypto-logo {
  opacity: 50%;
  position: fixed;
  width: 125px;
  bottom: 130px;
  right: 70px;
}
</style>
