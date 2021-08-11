<template>
  <h2>我是子級</h2>
  <h4>
    {{'我是在子級的: ' + JSON.stringify(repositories)}}
  </h4>
  <p>{{ manTitle + '(因為值不是響應式的，所以不會變動)' }}</p>
  <p>{{ womanTitle }}</p>
  <p>{{ childrenTitle }}</p>
  <p>{{ dogTitle }}</p>
  <p>{{ catTitle }}</p>

  <br>

  <button @click="handleGetNewPosts(3)">點我從子級獲取新Posts</button>
  <br>
  <br>
  <button @click="handleTitle">點我從子級更改dogTitle跟catTitle</button>
</template>

<script>
import { defineComponent, inject } from 'vue'

export default defineComponent({
  name: 'HelloWorldChild',
  props: {
    repositories: {
      type: Object,
      default: {}
    }
  },
  setup() {
    const getNewPosts = inject('getNewPosts')
    const manTitle = inject('manTitle')
    const womanTitle = inject('womanTitle', '哇哈哈') // '哇哈哈'，為默認值(可選)，僅在父級未提供對應的provide時觸發
    const childrenTitle = inject('childrenTitle')
    const dogTitle = inject('dogTitle')
    const catTitle = inject('catTitle')

    const handleGetNewPosts = (id) => {
      getNewPosts({id})
    }

    const handleTitle = () => {
      catTitle.value = '波斯貓-金毛' // 從子級修改了父級的catTitle內容
      dogTitle = '馬爾濟斯-大熊' // "dogTitle" is read-only
    }

    return {
      manTitle,
      womanTitle,
      childrenTitle,
      dogTitle,
      catTitle,
      handleGetNewPosts,
      handleTitle
    }
  }
})
</script>