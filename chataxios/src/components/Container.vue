<template>
  <div class="container">
    <slot>
      <ChatMessage></ChatMessage>
    </slot>
  </div>
    
</template>
    
<script>

import ChatMessage from './ChatMessage.vue'

export default {
  name: 'App',
  components: {
    ChatMessage,
  },
  data(){
    return {
      name:'Anton',
      date:'24.12',
    }
  }
}
</script>

<style>
.container {
  width: 764px;
  margin: auto;
  box-shadow: 0 0 15px 0 #5f5f5f73;
}
</style>
