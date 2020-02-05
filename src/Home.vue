<template>
  <div class="container">
    <UiButton @click="onClick" color='#2dada'
    :small='small'
    :normal='normal'
    :large='large'
    :xlarge='xlarge' circle >hello</UiButton>

    <div class="btn-group">
      <UiButton class="btn" @click="resize('small')">小</UiButton>
      <UiButton class="btn" @click="resize('normal')">正常</UiButton>
      <UiButton class="btn" @click="resize('large')">大</UiButton>
      <UiButton class="btn" @click="resize('xlarge')">超大</UiButton>
    </div>
  </div>

</template>
<script lang='ts'>
  import {Component, Vue} from 'vue-property-decorator'
  import UiButton from './components/UiButton.vue'

  @Component({
    components: {
      UiButton,
    },
  })
  export default class Home extends Vue{

    private small:boolean = false
    private normal:boolean = false
    private large:boolean = false
    private xlarge:boolean = false

    private resize(name: string){
      switch(name){
        case 'small':
          this.small = true
          this.normal = false
          this.large = false
          this.xlarge = false
          break;
        case 'normal':
          this.small = false
          this.normal = true
          this.large = false
          this.xlarge = false
          break;
        case 'large':
          this.small = false
          this.normal = false
          this.large = true
          this.xlarge = false
          break;
        case 'xlarge':
          this.small = true
          this.normal = false
          this.large = false
          this.xlarge = true
          break;
      }
    }
    private onClick(even: MouseEvent){
      window.console.log(even)
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
  .container
    .btn-group
      display flex
      margin-top 20px
      .btn
        margin-right 15px
</style>