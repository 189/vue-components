<template>
  <div :class="_clas" :style="style">
    <input 
      :value="value"
      :disabled="disabled" 
      :name="name" 
      :checked="checked"
      @change="changeHandler"
      type="checkbox"
      />
    <button type="button"></button>
  </div>
</template>

<script>
import { cssPrefix } from 'utils/variable.js'
import { base, input } from 'utils/mixins.js'
export default {
  mixins: [base, input],
  props: {
    checked: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    _clas () {
      return [cssPrefix + 'switch-wrapper', this.clas]
    }
  },
  data () {
    return {
      cssPrefix: cssPrefix
    }
  },
  methods: {
    changeHandler (e) {
      this.$emit('on-change', e.target.checked)
    }
  }
}
</script>

<style lang="scss">
  @import '~styles/variable.scss';
  @import '~styles/mixins.scss';
  .#{$css-prefix}{
    &switch-wrapper{
      position:relative;
      @include disabled;
      display:inline-block;
      vertical-align: middle;
      overflow:hidden;
      height: 32px;
      width: 50px;
      button{
        height:100%;
        border-radius:30px;
        background-color:$sub-color;
        margin: 0;
        padding: 0;
        transition:all 0.3s $ease-in-out;
        width:100%;
        position: relative;
        border:2px solid #999;
        box-sizing: border-box;
        &:before{
          content:'';
          height:100%;
          width:60%;
          border-radius:50%;
          background-color:#fff;
          left:0;
          top:0;
          position:absolute;
          transition:left 0.3s $ease-in-out;
        }
      }
      input{
        width:100%;
        height:100%;
        z-index:10;
        position:absolute;
        opacity:0;
        padding: 0;
        margin: 0;
        &:checked+button{
          background-color:$primary-color;
          border-color:$primary-color;
        }
        &:checked+button:before{
          left:40%;;
        }
      }
    }
  }
</style>
