<script lang="ts">
export default {
  data() {
    return {
      inputCmd: 'Hello',
      inputLastCmd: 'Hello',
      userMsg: 'guest',
      deviceMsg: 'term.arduc.ch',
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
        this.items.push({ type: false, message: ["Welcome on <strong>Artiom</strong> terminal website !",
        "Type 'help' to see list of available commands.",
        '--',
        "The project is created by Artiom Duc / Design inspired from M4TT72",
        '--']});
      } else if (cmd === 'help') {
        this.items.push({ type: false, message: ["Avaiable commands:",
        '<strong>hello</strong>',
        '<strong>help</strong>',
        '<strong>sudo</strong>',
        '<strong>date</strong>',
        '<strong>time</strong>',
        '<strong>weather</strong>',
        '<strong>about</strong>',
        '<strong>linkedin</strong>',
        '<strong>repo</strong>'] });
      } else if (cmd === 'repo') {
        this.items.push({ type: false, message: ['The repository: <a target="_blank" href="https://github.com/ArtiomInc/terminal">https://github.com/ArtiomInc/terminal</a>'] });
      } else if (cmd === "sudo") {
        this.items.push({ type: false, message: ['<pre>You are now logged in as root <strong>(wip)</strong></pre>'] });
      } else if (cmd === "date") {
        this.items.push({ type: false, message: ['<pre>Command not available yet: <strong>work in progress...</strong></pre>'] });
      } else if (cmd === "time") {
        this.items.push({ type: false, message: ['<pre>Command not available yet: <strong>work in progress...</strong></pre>'] });
      } else if (cmd === "weather") {
        this.items.push({ type: false, message: ['<pre>Command not available yet: <strong>work in progress...</strong></pre>'] });
      } else if (cmd === "about") {
        this.items.push({ type: false, message: ['<pre>Command not available yet: <strong>work in progress...</strong></pre>'] });
      } else if (cmd === "linkedin") {
        this.items.push({ type: false, message: ['<pre>Command not available yet: <strong>work in progress...</strong></pre>'] });
      } else if (cmd === "secret") {
        this.items.push({ type: false, message: ['<pre>Command not available yet: <strong>work in progress...</strong></pre>'] });
      } else {
        this.items.push({ type: false, message: ['Command not found: ' + "Type 'help' to see list of available commands."] });
      }
    }
  }
}
</script>

<template>
  <div ref="chat" class="card" @click="focusInput">
    <ul class="terminal">
      <li v-for="(item) in items" v-bind:key="item">
        <span v-if="item.type" class="user">{{ userMsg }}</span>
        <span v-if="item.type" class="at">@</span>
        <span v-if="item.type" class="device">{{ deviceMsg }}</span>
        <span v-if="item.type" class="two_points">$:&nbsp;</span>
        <span v-if="item.type" v-for="msg in item.message">{{ msg }}</span>
        <span v-if="item.type == false" v-for="msg in item.message" class="content_msg" v-html="msg"></span>
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
  border: 2px solid #00DC82;
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
  color: #00DC82;
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
