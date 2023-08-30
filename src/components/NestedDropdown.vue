<template>
  <b-dropdown ref="dropdown" class="dropdown" variant="link" toggle-class="text-decoration-none" no-caret @show="isFocus=true" @hidden="isFocus=false">
    <template #button-content>
      <b-form-input :value="value" :class="isFocus?'form-control-focus':''" class="text-center"></b-form-input>
    </template>
    <b-dropdown 
      v-for="(item,idx) in option" 
      :key="'dropdown-'+idx" 
      class="itemDropdown" 
      id="itemDropdown" 
      :text="item.title" 
      variant="link" 
      dropright no-caret
      ref="itemDropdown"
    >
      <template #button-content>
        <div @mouseover="onHover(idx)">
          <b-dropdown-item @click="returnObj(item.title)">{{item.title}}</b-dropdown-item>
        </div>
      </template>
      <b-dropdown-item v-for="(val,idx) in item.content" :key="'btn-'+idx" @click="returnObj(val)">{{val}}</b-dropdown-item>
    </b-dropdown>
  </b-dropdown>
</template>

<script>
export default {
  props:['option','value'],
  data:()=>({
    dropDownVisible:false,
    isFocus:false,
  }),
  computed:{
    inputData: {
      get: function() {
        return this.value
      },
      set: function(value) {
        this.$emit('input',value)
      }
    }
  },
  mounted() {
    this.$root.$on('bv::dropdown::show', bvEvent => {
      if(bvEvent.componentId === 'itemDropdown') {
        this.dropDownVisible = true;
      }
    })
    this.$root.$on('bv::dropdown::hide', bvEvent => {
      if(bvEvent.componentId === 'itemDropdown') {
        this.dropDownVisible = false;
      }
      if(this.dropDownVisible) {
        bvEvent.preventDefault()
      }
    })
  },
  methods:{
    onHover(idx){
      this.$refs.itemDropdown[idx].visible=true
    },
    returnObj(val){
      this.inputData = val
      this.$emit('returnObj',val)
      this.$refs.dropdown.visible=false
    }
  }
}
</script>

<style scoped>
::v-deep.dropdown .btn{
  padding: 0;
  text-decoration: none;
  text-align: left;
  color: #000;
}
::v-deep.dropdown .btn .dropdown-item:hover{
  background-color: #e9ecef;
  color: #000;
}
::v-deep.dropdown .btn .dropdown-item:active{
  background-color: #007bff;
  color: #fff;
}
::v-deep.dropdown .form-control:hover .dropdown-menu.show{
    display: block;
}
::v-deep.dropdown .form-control{
  cursor: pointer;
}
::v-deep.dropdown .form-control-focus{
  border-color: #80bdff;
  outline: 0;
  box-shadow: 0 0 0 0.2rem rgba(0, 123, 255, 0.25);
}
::v-deep.dropdown .dropdown-menu{
  min-width: auto;
  width:100%;
}
::v-deep.dropdown .dropdown-menu  div{
  width: 100%;
  text-align: left;
}
::v-deep.itemDropdown .dropdown-menu{
  min-width: auto;
  width:100%;
  transform: none !important;
  left: 100% !important;
}
::v-deep.itemDropdown .dropdown-menu .dropdown-item:hover{
  background-color: #e9ecef;
}
::v-deep.itemDropdown .dropdown-menu .dropdown-item:active{
  background-color: #007bff;
  color: #fff;
}
</style>