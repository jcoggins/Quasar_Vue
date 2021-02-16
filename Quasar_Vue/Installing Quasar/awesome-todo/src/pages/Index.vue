<template>
  <q-page  padding>
    <button style="position: absolute; right: 10px"
    @click="counter++">
      {{ counter }}
    </button>

    <!-- Binding Data to the view -->
    <input v-model="message"
    @keyup.esc="clearMessage"
    @keyup.enter="alertMessage"
    v-autofocus
    :class="{ 'error' : message.length > 22 }"
    ref="messageInput"
    />

    <button @click="clearMessage">Clear</button>
    <div>{{ message.length }}</div>
    <h5
    v-if="message.length"
    class="border-gray">{{ message }}</h5>
    <h6 v-else>No message available</h6>
    <hr>
    <p>Uppercase message: {{ this.messageUpperCase }} </p>
    <p>Lowercase message: {{ message | messageLowercase }} </p>
  </q-page>
</template>

<script>
  export default {
  /* Storing data msg*/
    data() {
      return {
        /* Property */
        message: 'Message to be bound',
        counter: 0
      }
    },
    computed: {
       messageUpperCase() {
        console.log('messageUpperCase was fired!')
        return this.message.toUpperCase() + this.counter;
      },
      errorStyle() {
        if (this.message.length > 22) {
          return {
            'color' : 'red',
            'background' : 'pink'
          }
        }
      }
    },
    methods: {
      clearMessage () {
        this.message = ''
      },
      alertMessage() {
        alert(this.message);
      },
    },
    filters: {
      messageLowercase(value) {
        return value.toLowerCase();
      }
    },
    directives: {
      autofocus: {
        inserted(el) {
          el.focus()
        }
      }
    },
    mounted() {
      this.$refs.messageInput.className = 'bg-green'
    },
  }
</script>

<style>
  .border-gray {
    border: 1px solid gray;
  }
  input, button {
    font-size: 23px;
  }
  .error {
    color: red;
    background: pink;
  }
</style>
