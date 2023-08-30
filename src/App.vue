<template>
  <div id="app">
    <div class="infoBox">
        <img src="./assets/logo.png"/>
        <h2 style="color:#333" class="mb-3">Nested Dropdown</h2>
        <b-button size="sm" class="m-2" style="background-color:#ce2f2f; border:0" href="https://www.npmjs.com/package/tag_transfer">Npm</b-button>
        <b-button size="sm" class="m-2" style="background-color:#333; border:0" href="https://github.com/wendy60113/TransferUI">Github</b-button>
    </div>
    <div class="demoBox">
      <VueLiveDemo
        :code="code"
        :show-code="showCode"
        :components="components"
      />
    </div>
  </div>
</template>

<script>
import VueLiveDemo from '@indielayer/vue-live-demo'
import DemoCode from "!!raw-loader!./view/DemoCode.vue"
import NestedDropdown from '@/components/NestedDropdown'
export default {
  name: 'App',
  data:()=>({
    showCode:true,
    code: DemoCode,
    components: {
      NestedDropdown
    },
  }),
  components:{
    VueLiveDemo
  }
}
</script>
<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Alata&display=swap');
#app{
  padding: 3% 10%;
}
.infoBox{
  width: 100%;
  text-align: center;
  font-family: 'Alata', sans-serif;
  img{
    margin: 10px;
    height: 40px;
  }
}
.demoBox{
  margin: 3% 0 0 0;
}
</style>
