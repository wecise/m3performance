<template>

  <div class="m3 m3performance" v-if="auth">
    <Header :auth="auth.signedUser" class="header"></Header>
    <div class="main">
      <SideBar class="sidebar" :auth="auth.signedUser" :global="global"></SideBar>
      <MainView :auth="auth" :global="global" class="content"></MainView>
    </div>
    <Footer :auth="auth.signedUser" class="footer"></Footer>
  </div>

</template>

<script>

import MainView from './components/MainView';
import Header from './components/layout/Header';
import SideBar from './components/layout/SideBar';
import Footer from './components/layout/Footer';

export default {
  name: 'app',
  components: {
    Header,
    MainView,
    SideBar,
    Footer
  },
  data(){
    return {
      global:null,
      auth: null
    }
  },
  created(){
    let init = ()=>{
        let timer = setInterval(()=>{
          try{
            this.m3.init();
            window.global = this.global = this.m3.global;
            this.auth = this.m3.auth;
            if(this.m3.auth && this.m3.global){
              clearTimeout(timer);
            }
          }catch(err){
            console.error(err);
          }
        },200);
    };
    
    init();
  }
}
</script>

<style>
  body{
    font-size: 12px;
    font-family: "PingFang SC",Arial,"Microsoft YaHei",sans-serif;
    margin: 0px;
    padding: 0px;
    overflow: hidden;
  }
  
  .el-menu .svg-icon{
    width: 1.2em!important;
    height: 1.2em!important;
    padding: 0px 5px 0 0;
  }

  .main{
    padding-top: 50px;
    display: flex;
  }
</style>
