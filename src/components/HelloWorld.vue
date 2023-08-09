<template>
  <q-page padding>
    <button style="position: absolute; right: 10px" @click="counter++">
      {{ counter }}
    </button>

    <input
      v-model="message"
      @keyup.esc="clearMessage"
      @keyup.enter="alertMessage"
      v-autofocus
      :style="errorStyle"
      ref="messageInput"
    />

    <div>{{ message.length }}</div>
    <button @click="clearMessage">Clear</button>
    <h5 class="border-grey" v-if="message.length">{{ message }}</h5>
    <h6 v-else>No message entered</h6>

    <hr />

    <p>Uppercase message: {{ messageUppercase }}</p>
    <p>Lowercase message: {{ message | messageLowercase }}</p>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      message: 'I love Vue.js so hard!',
      counter: 0,
    };
  },
  computed: {
    messageUppercase() {
      console.log('messageUppercase was fired');
      return this.message.toUpperCase() + this.counter;
    },
    errorStyle() {
      if (this.message.length > 22) {
        return {
          color: 'red',
          background: 'pink',
        };
      }
    },
  },
  methods: {
    clearMessage() {
      this.message = '';
    },
    alertMessage() {
      alert(this.message);
    },
  },
  filters: {
    messageLowerCase(value) {
      return value.toLowerCase();
    },
  },
  directives: {
    autofocus: {
      inserted(el) {
        el.focus();
      },
    },
  },
  beforeCreate() {
    console.log('beforeCreate');
  },
  created() {
    console.log('created');
  },
  beforeMount() {
    console.log('beforemounted');
  },
  mounted() {
    console.log(this.$refs);
    this.$refs.messageInput.className = 'bg-green';
  },
};
</script>

<style>
.border-grey {
  border: 1px solid grey;
}
input,
button {
  font-size: 23px;
}

.error {
  color: red;
  background: pink;
}
</style>
