<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <h1>
      {{ JSON.stringify(repositories) }}
    </h1>
    <button @click="handleGetNewPosts(1)">點我從父級獲取新Posts</button>
    <br>
    <br>
    <button @click="handleChangeTitle">點我從父級更改manTitle跟childrenTitle</button>
    <p>{{ childrenTitle }}</p>
    <p>{{ catTitle }}</p>
    <br>
    <br>

    <div>-----------------------------------</div>

    <HelloWorldChild :repositories="repositories" />
  </div>
</template>

<script>
import { defineComponent, provide, readonly, ref } from 'vue'
import useGetPosts from './useGetPosts.vue'

import HelloWorldChild from './HelloWorldChild.vue'

export default defineComponent({
  name: 'HelloWorld',
  components: {
    HelloWorldChild
  },
  props: {
    msg: String
  },
  setup(props, context) {
    const { repositories, getPosts } = useGetPosts()
    let manTitle = '新好男人' // 無響應式的值
    const childrenTitle = ref('新好小孩') // 建立響應式的值
    const dogTitle = ref('新好小狗')
    const catTitle = ref('新好小貓') // 建立響應式的值

    const handleGetNewPosts = (id) => {
      getPosts({id: id})
    }

    const handleChangeTitle = () => {
      childrenTitle.value = '蠟筆小新'
      manTitle = 'The Rock 巨石強森'

      console.log('manTitle', manTitle) // 在父級的manTitle變成了'The Rock 巨石強森'，但是子級的manTitle還是'新好男人'
    }

    provide('manTitle', manTitle) 
    // provide('womanTitle', '新好女人') // 對應到HelloWorldChild.vue
    provide('childrenTitle', childrenTitle)
    provide('dogTitle', readonly(dogTitle)) // readonly防止值被子級修改
    provide('catTitle', catTitle)
    provide('getNewPosts', getPosts)

    return {
      repositories,
      childrenTitle,
      catTitle,
      handleGetNewPosts,
      handleChangeTitle
    }
  }
})
</script>
