<template>
  <div id="app">
    <Container>
      <ChatWindow>
      </ChatWindow>
    </Container>
  </div>
</template>

<script>

import Container from './components/Container.vue'
import ChatWindow from './components/ChatWindow.vue'
//import ChatMessage from './components/ChatMessage.vue'

export default {
  name: 'App',
  components: {
    Container,
    ChatWindow,
    //ChatMessage,
  },
  data(){
    return {
    }
  },
}
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

body {
  margin: 0;
  background-color: #f9f9fa;
}
</style>
