<template>
  <div id="cl">
      <slot></slot>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">
    #cl{
         display: inline-block;
          width: 20px;
          height: 20px;
          line-height: 20px;
          text-align: center;
          border: 1px solid black;
    }
</style>