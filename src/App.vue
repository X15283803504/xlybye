<template>
  <div id="app">
    <!--显示组件容器-->
    <router-view></router-view>
    <tabbar v-if="$route.name == 'index' || $route.name == 'list' ||$route.name == 'orderform' ||$route.name == 'login' "></tabbar>
  </div>
</template>

<script>
import tabbar from "./views/tabbar";
export default {
  components:{
    "tabbar":tabbar
  },
  methods:{
    // 购物车数量
    cartCount(){
      var url="cartcount";
      this.axios.get(url).then(res=>{
        if(res.data.code==-1){
          this.$store.state.cartCount=0;
        }else{
          this.$store.state.cartCount=res.data.data.length;
        }
      })
    },
    // 登录状态 检测当前是否有用户登录
    state(){
      var url="state";
      this.axios.get(url).then(res=>{
        if(res.data.code==-1){  //未登录
          this.$store.state.show=false;
        }else{                  //已登录
           this.$store.state.show=true;
           this.$store.state.np=res.data.data[0];
        }
      })
    },
  },
  created(){
      this.state();
      this.cartCount();
  }
}
</script>

<style>

</style>
