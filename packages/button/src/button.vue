<template>
  <div>
    <button @click="handleClick">
      <slot></slot>
    </button>
  </div>
</template>

<script>
export default {
  name: 'LgButton',
  methods: {
    handleClick(evt) {
      this.$emit('click', evt)
      // 阻止表单的默认事件
      evt.preventDefault()
    }
  }
}
</script>

<style>

</style>