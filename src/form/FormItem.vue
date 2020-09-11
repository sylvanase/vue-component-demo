<template>
  <div>
    <label>{{ label }}</label>
    <div>
      <slot ></slot> 
      <!-- 显示验证失败的原因 -->
      <p v-if="errMessage">{{ errMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LgFormItem',
  props: {
    label: {
      type: String
    },
    prop: {
      type: String
    }
  },
  data () {
    return {
      errMessage: ''
    }
  }
}
</script>

<style>

</style>