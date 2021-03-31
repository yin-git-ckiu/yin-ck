<template>
  <div id="num">
    <slot></slot>
  </div>
</template>

<script>
export default {
    name:'num',

}
</script>

<style lang="scss">
        #num{
            display: inline-block;
            width: 30px;
            height: 30px;
        }
</style>