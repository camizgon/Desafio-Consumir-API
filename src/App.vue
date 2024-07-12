<template>
  <section class="chat-container">
    <UserInput
      v-for="(user, index) in misFunciones"
      :key="index"
      :user="user"
      @send-message="addMessage"
    />
    <ChatApp :messages="messages" />
  </section>
</template>

<script>
import axios from 'axios';
import UserInput from './components/UserInput.vue';
import ChatApp from './components/ChatApp.vue';

export default {
  name: 'App',
  components: {
    UserInput,
    ChatApp
  },
  data() {
    return {
      rawUsers: [],
      messages: []
    };
  },
  async mounted() {
    try {
      const { data: data1 } = await axios.get("https://randomuser.me/api/");
      const { data: data2 } = await axios.get("https://randomuser.me/api/");
      this.rawUsers = [data1.results[0], data2.results[0]];
    } catch (error) {
      console.log(error);
      alert("Error en la petición");
    }
  },
  computed: {
    misFunciones() {
      return this.rawUsers.map(user => ({
        name: `${user.name.first} ${user.name.last}`,
        email: user.email,
        picture: user.picture.large
      }));
    }
  },
  methods: {
    addMessage(message) {
      this.messages.push(message);
    }
  }
};
</script>

<style>
.chat-container {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 20px;
}
</style>


