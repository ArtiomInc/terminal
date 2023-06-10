<script lang="ts">
export default {
  data() {
    return {
      inputCmd: "Hello",
      inputLastCmd: "Hello",
      userMsg: "guest",
      deviceMsg: "term.arduc.ch",
      items: [],
    };
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
      this.inputCmd = "";
      this.$nextTick(() => {
        this.scrollToBottom();
      });
    },
    remember() {
      this.inputCmd = this.inputLastCmd;
    },
    sendCmd(cmd) {
      if (cmd === "hello") {
        this.items.push({
          type: false,
          message: [
            "Welcome on <strong>Artiom</strong> terminal website !",
            "Type 'help' to see list of available commands.",
            "--",
            "The project is created by Artiom Duc / Design inspired from M4TT72",
            "--",
          ],
        });
      } else if (cmd === "help") {
        this.items.push({
          type: false,
          message: [
            "Avaiable commands:",
            "<strong>hello</strong>",
            "<strong>help</strong>",
            "<strong>sudo</strong>",
            "<strong>date</strong>",
            "<strong>time</strong>",
            "<strong>about</strong>",
            "<strong>secret</strong>",
            "<strong>linkedin</strong>",
            "<strong>repo</strong>",
          ],
        });
      } else if (cmd === "repo") {
        this.items.push({
          type: false,
          message: [
            'The repository: <a target="_blank" href="https://github.com/ArtiomInc/terminal">https://github.com/ArtiomInc/terminal</a>',
          ],
        });
      } else if (cmd === "sudo") {
        window.open("https://youtu.be/dQw4w9WgXcQ", "_blank");
        this.items.push({
          type: false,
          message: ["<pre>Oops !</pre>"],
        });
      } else if (cmd === "time") {
        const today = new Date();
        const time =
          today.getHours() +
          ":" +
          today.getMinutes() +
          ":" +
          today.getSeconds();
        this.items.push({
          type: false,
          message: ["Current time: " + time],
        });
      } else if (cmd === "date") {
        const today = new Date();
        const date =
          today.getDate() +
          "." +
          (today.getMonth() + 1) +
          "." +
          today.getFullYear();
        this.items.push({
          type: false,
          message: ["Today date: " + date],
        });
      } else if (cmd === "about") {
        this.items.push({
          type: false,
          message: [
            "<pre>Hey ! I'm Artiom, Industrial Systems Technician, based in Switzerland.</br>Type linkedin command to get my link profile.</pre>",
          ],
        });
      } else if (cmd === "linkedin") {
        this.items.push({
          type: false,
          message: [
            'My linkedin profile: <a target="_blank" href="https://www.linkedin.com/in/artiom-duc/">https://www.linkedin.com/in/artiom-duc/</a>',
          ],
        });
      } else if (cmd === "music") {
        this.items.push({
          type: false,
          message: [
            "<pre>Command not available yet: <strong>work in progress...</strong></pre>",
          ],
        });
      } else if (cmd === "secret") {
        window.open("https://youtu.be/cLhY_DSYaWM", "_blank");
        this.items.push({
          type: false,
          message: [
            "<pre>Grigori Efimovich Rasputin was a Russian mystic and healer.</pre>",
          ],
        });
      } else if (cmd === "") {
      } else {
        this.items.push({
          type: false,
          message: [
            "'" +
              cmd +
              "' is not recognized as an internal or external command</br>type 'help' to see list of available commands.",
          ],
        });
      }
    },
  },
};
</script>

<template>
  <div ref="chat" class="card" @click="focusInput">
    <ul class="terminal">
      <li v-for="item in items" v-bind:key="item">
        <span v-if="item.type" class="user">{{ userMsg }}</span>
        <span v-if="item.type" class="at">@</span>
        <span v-if="item.type" class="device">{{ deviceMsg }}</span>
        <span v-if="item.type" class="two_points">$:&nbsp;</span>
        <span v-if="item.type" v-for="msg in item.message">{{ msg }}</span>
        <span
          v-if="item.type == false"
          v-for="msg in item.message"
          class="content_msg"
          v-html="msg"
        ></span>
      </li>
      <li ref="li_bottom" class="input">
        <span class="user">{{ userMsg }}</span>
        <span class="at">@</span>
        <span class="device">{{ deviceMsg }}</span>
        <span class="two_points">$:&nbsp;</span>
        <input
          ref="command"
          v-model="inputCmd"
          @keydown.enter="add"
          @keydown.up="remember"
        />
      </li>
    </ul>
  </div>
</template>

<style scoped>
.card {
  height: calc(100vh - 14px);
  width: calc(100vw - 14px);
  margin: 7px;
  border: 2px solid #00dc82;
  border-radius: 5px;
  overflow: auto;
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
}
.card::-webkit-scrollbar {
  /* Chrome, Safari and Opera */
  display: none;
}
.terminal {
  list-style-type: none;
  margin: 20px;
}
.content_msg {
  display: block;
  margin: 0;
  padding: 0;
}
.user {
  color: #00dc82;
}
.device {
  color: #6792c7;
}
.input {
  display: flex;
}
input {
  background-color: transparent;
  width: 100%;
  border: 0;
  outline: 0;
}
</style>
