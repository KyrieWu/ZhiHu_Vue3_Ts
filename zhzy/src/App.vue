<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <!-- <column-list :list="list"></column-list> -->
    <validate-form @form-submit="onFormSubmit">
      <div class="mb-3">
        <label class="form-label">邮箱地址</label>
        <validate-input
          :rules="emailRules"
          v-model="emailVal"
          placeholder="请输入邮箱地址"
          type="text"
          ref="inputRef"
        ></validate-input>
        {{ emailVal }}
      </div>
      <div class="mb-3">
        <label class="form-label">密码</label>
        <validate-input
          :rules="passwordRules"
          v-model="passwordVal"
          placeholder="请输入密码"
          type="password"
        ></validate-input>
      </div>
      <template #submit><span class="btn btn-danger">Submit</span> </template>
    </validate-form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/Columnlist.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
import ValidateForm from './components/ValidateForm.vue'
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: '这里是test1的专栏',
    avatar: '@/assets/logo.png'
  },
  {
    id: 1,
    title: 'test2的专栏',
    description: '这里是test2的专栏',
    avatar: '../assets/logo.png'
  },
  {
    id: 1,
    title: 'test2的专栏',
    description: '这里是test2的专栏,adfjajdfkjakdjfkajdkjfkajdkf'
    // avatar: '../assets/logo.png'
  },
  {
    id: 1,
    title: 'test2的专栏',
    description: '这里是test2的专栏',
    avatar: '../assets/logo.png'
  }
]
const currentUser: UserProps = {
  isLogin: true,
  name: 'viking'
}
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader,
    ValidateInput,
    ValidateForm
  },
  setup () {
    const inputRef = ref<any>()
    const emailVal = ref('13@test.com')
    const passwordVal = ref('')
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }
    ]
    const passwordRules: RulesProp = [
      { type: 'required', message: '密码不能为空' }
    ]
    const onFormSubmit = (result: boolean) => {
      console.log(inputRef.value.validateEmail())
    }
    return {
      list: testData,
      currentUser: currentUser,
      emailRules,
      emailVal,
      passwordRules,
      passwordVal,
      onFormSubmit,
      inputRef
    }
  }
})
</script>

<style>
</style>
