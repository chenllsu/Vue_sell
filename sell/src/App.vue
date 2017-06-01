<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
       <router-link to="/ratings">评论</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
// type="text/ecmascript-6"
  import header from './components/header/header';
  const ErrOK = 0;
  export default {
    data () {
      return {
        seller: {}
      };
    },
    mounted: function () {
      console.log('APP.vue create...');
      this.$http.get('/api/seller').then(function (response) {
        response = response.body;
        console.log(response);
        if (response.errno === ErrOK) {
          this.seller = response.data;
          console.log(this.seller);
        }
      });
    },
    // name: 'app',
    components: {
      'v-header': header
    }
  };
</script>

<style>
  #app .tab {
    display: flex;
    height: 80px;
  }
  .tab-item{
    flex: 1;
    text-align: center;
    line-height: 80px;
  }
</style>
