<template>
    <div class="chat-window">
    <div class="chat-messages">
      <div class="scroll-wrapper">
        <slot v-for="(message) in listMessages">
            <ChatMessage :username="message['author']" :datetime="message['datetime']" :mes="message['text']"></ChatMessage>
        </slot>
      </div>
    </div>
    <div class="chat-send-panel">
      <input type="text" placeholder="Ваш никнейм..." class="chat-send-name-field" v-model="form.author"/>
      <input type="text" placeholder="Сообщение..." class="chat-send-message-field" v-model="form.text"/>
      <button @click="sendMessage()">
        <img src="/img/send.png" />
      </button>
    </div>
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
      listMessages: this.getMessage(),
      form: {
        text: null,
        author: null,
      }
    }
  },
  methods:{
    getMessage(){
      this.axios.get('https://61bcd385d8542f0017824a2a.mockapi.io/messages')
        .then((response) => {
          this.listMessages = response['data'];
          
          //console.log(this.listMessages['0']['author']);
        })
    },

    sendMessage(){
      this.axios.post('https://61bcd385d8542f0017824a2a.mockapi.io/messages', this.form);
      console.log(this.form.text);
      this.getMessage();
    },
  },
  mounted(){
    this.getMessage();

    setInterval(() => {
      this.getMessage();
    },1000 * 10);
    }
  }
  
</script>


<style scoped>
    .chat-window {
    width: 100%;
    height: 100vh;
    }
    .chat-messages {
    width: 100%;
    background-color: #e9f3fa;
    background-image: url("/img/blue-snow.png");
    overflow: auto;
    height: calc(100vh - 60px);
    box-sizing: border-box;
    }
    .chat-messages .scroll-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: flex-end;
    padding: 20px;
    min-height: calc(100vh - 60px);
    box-sizing: border-box;
    }
    .chat-send-panel {
    width: 100%;
    height: 60px;
    box-sizing: border-box;
    background-color: #dfe9f0;
    display: flex;
    padding: 5px;
    justify-content: space-between;
    align-items: center;
    }
    .chat-send-panel input,
    .chat-send-panel button {
    border-radius: 50px;
    color: #3a4158;
    font-size: 14px;
    border: 0;
    }
    .chat-send-panel input {
    border: 2px solid #bbb;
    padding: 10px 20px;
    }
    .chat-send-message-field {
    flex-grow: 1;
    }
    .chat-send-name-field {
    width: 100px;
    flex-grow: 0;
    }
    .chat-send-panel button {
    background-color: transparent;
    padding: 10px;
    cursor: pointer;
    transition: 0.2s;
    }
    .chat-send-panel button:active {
    transform: scale(0.9);
    }
    .chat-send-panel button img {
    width: 100%;
    }
</style>