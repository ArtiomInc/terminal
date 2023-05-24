<script lang="ts">
import { ref, provide } from 'vue'
export default {
  data() {
    return {
      test: '<br>',
      inputCmd: 'Hello',
      inputLastCmd: 'Hello',
      userMsg: 'guest',
      deviceMsg: 'terminal.arduc.ch',
      items: [],
    }
  },
  mounted() {
    this.add();
    this.focusInput();
  },
  methods: {
    focusInput() {
      this.$refs.command.focus();
    },
    scrollToBottom() {
      const chatContainer = this.$refs.chat;
      chatContainer.scrollTop = chatContainer.scrollHeight;
    },
    add() {
      this.items.push({ type: true, message: this.inputCmd });
      this.sendCmd(this.inputCmd.toLowerCase());
      this.inputLastCmd = this.inputCmd;
      this.inputCmd = '';  this.$nextTick(() => {
        this.scrollToBottom();
      });
    },
    remember() {
      this.inputCmd = this.inputLastCmd;
    },
    sendCmd(cmd) {
      if (cmd === 'hello') {
        this.items.push({ type: false, message: ["Type 'help' to see list of available commands.",
        '--',
        "The project is from Artiom Duc ❤️ type 'repo' to check out the repository.",
        '--']});
      } else if (cmd === 'help') {
        this.items.push({ type: false, message: ["Avaiable commands:",
                                                '<strong>hello</strong> - Say hello to terminal',
                                                '<strong>help</strong> - List all commands',
                                                '<strong>repo</strong> - Give repository'] });
      } else if (cmd === 'repo') {
        this.items.push({ type: false, message: ['The original repo: <a target="_blank" href="https://github.com/ArtiomInc/terminal">https://github.com/ArtiomInc/terminal</a>'] });
      } else if (cmd === 'test') {
        this.items.push({ type: false, message: ['<pre>   f    t </pre>'] });
      } else {
        this.items.push({ type: false, message: ['unknown command<br>' + "Type 'help' to see list of available commands."] });
      }
    }
  }
}
</script>

<template>
  <div ref="chat" class="card" @click="focusInput">
    <ul class="terminal">
      <li v-for="(item) in items">
        <span v-if="item.type" class="user">{{ userMsg }}</span>
        <span v-if="item.type" class="at">@</span>
        <span v-if="item.type" class="device">{{ deviceMsg }}</span>
        <span v-if="item.type" class="two_points">$:&nbsp;</span>
        <span v-if="item.type" v-for="(msg) in item.message">{{ msg }}</span>
        <span v-if="item.type == false" v-for="(msg) in item.message" class="content_msg" v-html="msg"></span>
      </li>
      <li ref="li_bottom" class="input">
        <span class="user">{{ userMsg }}</span>
        <span class="at">@</span>
        <span class="device">{{ deviceMsg }}</span>
        <span class="two_points">$:&nbsp;</span>
        <input ref="command" v-model="inputCmd" @keydown.enter="add" @keydown.up="remember"/>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.card{
  height: calc(100vh - 14px);
  width: calc(100vw - 14px);
  margin: 7px;
  border: 2px solid #d79921;
  border-radius: 5px;
  overflow: auto;
  -ms-overflow-style: none;  /* IE and Edge */
  scrollbar-width: none;  /* Firefox */
}
.card::-webkit-scrollbar { /* Chrome, Safari and Opera */
  display: none;
}
.terminal {
  list-style-type: none;
  margin: 20px
}
.content_msg {
  display: block;
  margin: 0;
  padding: 0;
}
.user{
  color: #8ae234;
}
.device{
  color: #6792c7;
}
.input{
  display: flex;
}
input {
  background-color: transparent;
  width: 100%;
  border: 0;
  outline: 0;
}
</style>
