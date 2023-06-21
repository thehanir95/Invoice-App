<template>
  <div>
    <div v-if="!isMobile" class="app">
      <Navigation/>
      <div class="app-content-main">
        <div class="app-content">
          <transition name="invoice">
            <InvoiceModal v-if="invoiceModal"/>
          </transition>
        <router-view/>
      </div>
      </div>
    </div>
    <div v-else class="support-msg">
      <h2>Sorry this app is not supported mobile devices.</h2>
    </div>
  </div>
</template>

<script>
import Navigation from "./components/Navigation.vue"
import InvoiceModal from '@/components/InvoiceModal'
import { mapState } from 'vuex'
export default {
  name: 'App',
  components: {
    Navigation,
    InvoiceModal
  },
  data(){
    return{
      isMobile: null
    }
  },
  created(){
    this.checkScreen();
    window.addEventListener("resize", this.checkScreen)
  },
  computed:{
    ...mapState(['invoiceModal'])
  },
  methods:{
    checkScreen() {
      const windowWidth = window.innerWidth;
      if (windowWidth <=750) {
        this.isMobile = true;
        return;
      }
      this.isMobile = false;
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,300;0,400;1,400&display=swap');
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  background-color: #1e2139;
}
.app-content-main{
  width: 100%;
  padding: 50px;
}
.app-content{
  margin-top: 16px;
  position: relative;
}
.app{
  display: flex;
  background: #141625;
  min-height: 100vh;
}
body{
  background-color: #1e2139;
  margin: 0;
}
.support-msg{
  display: flex;
  justify-content: center;
  align-items: center;
  justify-items: center;
  height: 100vh;
}

.invoice-enter-active,
.invoice-leave-active{
  transition: 0.8s ease all;
}

.invoice-enter-from,
.invoice-leave-to{
  transform: translateX(-700px);
}
</style>
