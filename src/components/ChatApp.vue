<template>
  <div class="chat-app">
    <div v-for="(message, index) in messages" :key="index" :class="{'user-message': message.user}">
      <span>{{ message.user.name }}</span>
      <span :style="{ backgroundColor: message.color, borderRadius: '10px', padding: '5px' }">{{ message.text }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ChatApp',
  props: {
    messages: {
      type: Array,
      required: true
    }
  }
};
</script>

<style>
.chat-app {
  position: absolute;
  margin-top: 15px;
  margin-left: 350px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 2px 2px 2px 2px #393d42 ;
  background-color: #eeeeee;
  padding: 10px;
  width: 500px;
  height: 320px;
  overflow: auto, scroll;
}
.user-message {
  display:flex;
  flex-direction: column;
  margin-bottom: 10px;

}
</style>