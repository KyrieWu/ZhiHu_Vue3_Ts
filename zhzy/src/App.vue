<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <column-list :list="list"></column-list>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/Columnlist.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
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
  isLogin: true
}
export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader
  },
  setup () {
    return {
      list: testData,
      currentUser: currentUser
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
