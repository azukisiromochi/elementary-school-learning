<template>
  <div class="container">
    <div v-if="multiplier">
      <p class="subtitle">3.14 × {{multiplier}} =</p>
      <van-button 
        type="primary" 
        round 
        @click="showPopup">
        Next
      </van-button>
      <van-popup 
        v-model="show" 
        closeable
        position="bottom"
        :style="{ height: '30%' }"
        @close="closePopup">
        <div><p class="subtitle">{{product}}</p></div>
      </van-popup>
    </div>
    <div v-if="!multipliers.length">
      <p class="subtitle">お疲れ様でした！</p>
      <van-button 
        type="warning" 
        round 
        @click="back">
        戻る
      </van-button>
      <van-button 
        type="primary" 
        round 
        @click="reload">
        もう一度
      </van-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PiePage',
  data() {
    return {
      show: false,
      multipliers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      multiplier: undefined,
      product: undefined,
      randomIndex: undefined,
    }
  },
  mounted() {
    this.doMultiplication()
  },
  methods: {
    showPopup() {
      this.show = true;
    },
    closePopup() {
      this.reset()
      this.doMultiplication()
    },
    reset() {
      this.multipliers.splice(this.randomIndex, 1)
      this.multiplier = undefined
      this.product = undefined
      this.randomIndex = undefined
    },
    doMultiplication() {
      setTimeout(() => {
        this.randomIndex = Math.floor(Math.random() * this.multipliers.length)
        this.multiplier = this.multipliers[this.randomIndex]
        this.product = Number((3.14 * this.multiplier).toFixed(2))
      }, 200)
    },
    back() {
      this.$router.push('/')
    },
    reload() {
      location.reload()
    }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: Quicksand, 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
