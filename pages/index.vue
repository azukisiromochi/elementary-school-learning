<template>
  <div class="container">
    <van-divider>算数</van-divider>
    <div>
      <van-button 
        type="primary" 
        round 
        @click="goNext('pie')">
        円周率の段
      </van-button>
    </div>
    <van-divider>社会</van-divider>
    <div>
      <van-button 
        type="warning" 
        round 
        @click="goNext('meiji1')">
        明治時代①
      </van-button>
      <van-button 
        type="warning" 
        round 
        @click="goNext('meiji2')">
        明治時代②
      </van-button>
      <van-button 
        type="warning" 
        round 
        @click="goNext('taisho')">
        大正時代
      </van-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  methods: {
    goNext(pageName) {
      this.$router.push('/' + pageName)
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
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

.van-divider {
  width: 80vw;
}
</style>
