<template>
  <div>
    <button class='ui-btn' @click="btnClick"
    :class="{
      'ui-btn-small': small,
      'ui-btn-normal': normal,
      'ui-btn-large': large,
      'ui-btn-xlarge': xlarge,
      'ui-btn-tile': tile,
      'ui-btn-rounded': rounded,
      'ui-btn-circle': circle,
      'ui-btn-disable': disable
    }"
    :style="`
      --color-tint:${TintColor}
    `"
    >
      <slot>Button</slot>
    </button>
  </div>
</template>
<script lang='ts'>
  import {Vue, Component, Emit, Prop} from 'vue-property-decorator'

  @Component
  export default class UiButton extends Vue{
    // 会从home获取到boolean值
    @Prop(Boolean) private small: boolean | undefined
    @Prop(Boolean) private normal: boolean | undefined
    @Prop(Boolean) private large: boolean | undefined
    @Prop(Boolean) private xlarge: boolean | undefined
    @Prop(Boolean) private tile: boolean | undefined
    @Prop(Boolean) private rounded: boolean | undefined
    @Prop(Boolean) private circle: boolean | undefined
    @Prop(Boolean) private disable: boolean | undefined
    @Prop(String) private color: string | undefined


    private get TintColor(){
      if(this.color){
        return this.color
      }else{
        return '#2d8cf0'
      }
    }

    // 执行btnClick调用emitClickEvent函数，并通过emitClickEvent发送click事件并且把参数一并发送出去
    @Emit('click') private emitClickEvent(even: MouseEvent){} // 这一行等价于this.$emit('click')

    private btnClick(even: MouseEvent){
      if(!this.disable){
        this.emitClickEvent(even)
      }
    }
  }
</script>
<style lang="stylus" rel="stylesheet/stylus" scoped>
  resize(min-width, height, paddingR, fontSize)
    min-width min-width
    height height
    padding 0 paddingR
    font-size fontSize
    &.ui-btn-rounded, &.ui-btn-circle
      border-radius (@height / 2)
    &.ui-btn-circle
      min-width @height
      padding 0px 0px
  .ui-btn
    resize(64px, 36px, 16px, 0.875rem)
    border 0 solid black
    border-radius 4px
    text-align center
    outline none
    font-weight 500
    letter-spacing 0.09em
    background-color var(--color-tint)
    cursor pointer
    user-select none
    &:hover
      filter brightness(120%)
    &:active
      filter brightness(80%)
    &.ui-btn-small
      resize(36px, 20px, 9px, 0.625rem)
    &.ui-btn-large
      resize(78px, 44px, 19px, 0.875rem)
    &.ui-btn-xlarge
      resize(92px, 52px, 23px, 1rem)
    &.ui-btn-tile
      border-radius 0
    &.ui-btn-disable
      cursor not-allowed
      background-color #f5f5f5
      color #c5c8ce
</style>
