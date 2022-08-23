<template>
  <div class="validate-input-container pb-3">
    <input
      class="form-control"
      :class="{ 'is-invalid': emailRef.error }"
      :value="emailRef.val"
      @blur="validateEmail"
      @input="updateValue"
      v-bind="$attrs"
    />
    <span v-if="emailRef.error" class="invalid-feedback">{{
      emailRef.message
    }}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, PropType, reactive } from 'vue'
import { emitter } from './ValidateForm.vue'
const emailReg = /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+((\.[a-zA-Z0-9_-]{2,3}){1,2})$/
interface RuleProp {
  type: 'required' | 'email';
  message: string
}

export type RulesProp = RuleProp[]
export default defineComponent({
  props: {
    rules: Array as PropType<RulesProp>,
    modelValue: String
  },
  inheritAttrs: false,
  setup (props, context) {
    const emailRef = reactive({
      val: props.modelValue || '',
      error: false,
      message: ''
    })
    const updateValue = (e: KeyboardEvent) => {
      const targetValue = (e.target as HTMLInputElement).value
      emailRef.val = targetValue
      context.emit('update:modelValue', targetValue)
    }
    const validateEmail = () => {
      if (props.rules) {
        const allPassed = props.rules.every(rule => {
          let passed = true
          emailRef.message = rule.message
          switch (rule.type) {
            case 'required' :
              passed = (emailRef.val.trim() !== '')
              break
            case 'email' :
              passed = emailReg.test(emailRef.val)
              break
            default:
              break
          }
          return passed
        })
        emailRef.error = !allPassed
        return allPassed
      }
      return true
    }
    onMounted(() => {
      emitter.emit('form-item-created', validateEmail)
    })

    return {
      emailRef,
      validateEmail,
      updateValue
    }
  }
})
</script>

<style>
</style>
