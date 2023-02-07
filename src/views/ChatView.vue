<template>
  <main>
    <div class="main_title">
      <h1>Chat</h1>
    </div>
    <div class="">
      <div class="">
        <input
          type="text"
          v-model="pseudo"
          class="form-control"
          placeholder="Votre pseudo"
        />
        <input
          type="text-area"
          v-model="message"
          class="form-control"
          placeholder="Votre message"
        />
        <input type="color" v-model="color" class="form-control" />
        <input
          type="button"
          Value="Envoyer"
          class="form-control"
          placeholder="Votre message"
          @click="sendMessage()"
        />
      </div>
    </div>
    <div class="chatBox" ref="chatBox">
      <div v-for="(row, index) in msg" v-bind:key="index" class="chat">
        <span class="pseudo" :style="{ color: row.color }">{{ row.pseudo }}</span
        >: {{ row.message }}
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      pseudo: "",
      message: "",
      color: "",
      msg: [],
    };
  },
  methods: {
    sendMessage() {
      this.msg.push({
        pseudo: this.pseudo,
        message: this.message,
        color: this.color,
      });
      this.message = "";
      this.$nextTick(() => {
        this.$refs.chatBox.scrollTop = this.$refs.chatBox.scrollHeight;
      });
      console.log(this.msg);
    },
  },
};
</script>

<style>
.chatBox {
  height: 300px;
  background-color: var(--main-white_color);
  overflow: scroll;
  margin: 50px 0;
  padding: 0 20px;
}
.chat {
  background-color: var(--main-white_color);
  color: var(--main-dark_color);
  text-align: left;
}

.pseudo {
  font-weight: bold;
}
</style>