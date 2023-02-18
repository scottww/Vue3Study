<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3.0 + Vite" />
  <h1>虚拟列表</h1>
  <VirtualList />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import VirtualList from './components/VirtualList.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    VirtualList
  }
}
</script>
