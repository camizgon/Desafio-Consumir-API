<template>
  <div class="user-input">
    <div class="card">
      <img :src="user.picture" alt="User photo">
      <p>{{ user.name }}</p>
      <textarea
        id="box-message"
        v-model="message"
        placeholder="Escribir Mensaje"
        @keyup.enter="sendMessage">
</textarea>
      <input id="box-color" type="color" v-model="color">
      <button @click="sendMessage">Envíar</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserInput',
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      message: '',
      color: '#ffffff'
    };
  },
  methods: {
    sendMessage() {
      if (this.message.trim()) {
        this.$emit('send-message', {
          user: this.user,
          text: this.message,
          color: this.color
        });
        this.message = '';
      }
    }
  }
};
</script>

<style>
.user-input {
  width: 15%;
  height: 30%;
  padding-left: 50px;
  padding-right: 50px;
}

.user-input img {
  width: 100%;
  margin-right: 10px;
  box-shadow: 2px 2px 2px 2px #393d42;
  border-radius: 5px;
  object-fit: cover;
}

p {
  text-align: center;
  font-weight: bolder;
}

#box-message {
  width: 95%;
  height: 105px;
}

#box-color {
  width: 100%;
  margin-top: 10px;
}

button {
  width: 100%;
  margin-top: 10px;
  transition: background-color 0.3s, color 0.3s;
}

button :hover{
  background-color: #717171;
}
</style>