<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <!-- <column-list :list="list"></column-list> -->
    <router-view></router-view>
    <footer class="text-center py-4 text-secondary bg-light mt-6">
      <small>
        <ul class="list-inline mb-0">
          <li class="list-inline-item">2020 者也专栏</li>
          <li class="list-inline-item">课程</li>
          <li class="list-inline-item">文档</li>
          <li class="list-inline-item">联系</li>
          <li class="list-inline-item">更多</li>
        </ul>
      </small>
    </footer>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/Columnlist.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: '这里是test1的专栏',
    avatar: ''
  },
  {
    id: 2,
    title: 'test2的专栏',
    description: '这里是test2的专栏',
    avatar: ''
  },
  {
    id: 3,
    title: 'test3的专栏',
    description: '这里是test3的专栏,adfjajdfkjakdjfkajdkjfkajdkf'
    // avatar: '../assets/logo.png'
  },
  {
    id: 4,
    title: 'test4的专栏',
    description: '这里是test4的专栏',
    avatar: ''
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
    GlobalHeader
  },
  setup () {
    const inputRef = ref<any>()
    return {
      list: testData,
      currentUser: currentUser,
      inputRef
    }
  }
})
</script>

<style>
</style>
