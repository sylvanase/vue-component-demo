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
import AsyncValidator from 'async-validator'
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
  inject: ['form'],
  data () {
    return {
      errMessage: ''
    }
  },
  mounted(){
    // 渲染完毕，注册validate事件，内部调用validate方法
    this.$on('validate', () => {
      this.validate()
    })
  },
  methods: {
    validate () {
      if(!this.prop) return
      // form中验证规则和数据
      const value = this.form.model[this.prop]
      const rules = this.form.rules[this.prop]

      // 验证的属性名及对象
      const descriptor = { [this.prop]: rules }
      const validator = new AsyncValidator(descriptor)

      return validator.validate({ [this.prop]: value }, errors => {
        if (errors) {
          this.errMessage = errors[0].message
        } else {
          this.errMessage = ''
        }
      })
    }
  }
}
</script>

<style>

</style>