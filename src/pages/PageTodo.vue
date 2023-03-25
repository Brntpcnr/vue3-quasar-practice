<template>
  <q-page padding>
    <button
    style="position: absolute; right: 10px"
    @click="counter++"
    >
    {{ counter }}
    </button>

    <input
    v-model="message"
    @keyup.esc="clearMessage"
    @keyup.enter="alertMessage"
    v-autofocus
    :style="errorStyle"
    ref="messageInput" />

    <button @click="clearMessage">Clear</button>

    <div>{{ message.length }}</div>

    <h5
    v-if="message.length"
    class="border-grey" >{{message}}</h5>
    <h6 v-else>No message entered :D</h6>

    <hr>

    <p>Uppercase message: {{ messageUppercase }} </p>
    <p>Lowercase message: {{ messageLowercase }} </p>

  </q-page>
</template>

<script>
export default {               //v-else works like an else in an if situation
  data() {
    return {
      message: "I love Vue.js so much!",
      counter: 0
    }
  },                           //filters can be used as well, basically they are methods with values specified to them however they are removed from vue3
  computed: {                  //Computed Properties can be used to calculate and display values based on a specific value or set of values in the data model
    messageUppercase() {
      console.log('messageUppercase was fired')
      return this.message.toUpperCase()
    },
    messageLowercase() {
      return this.message.toLowerCase()
    },
    errorStyle() {
      if (this.message.length > 22) {
        return {
          'color' : ' red',
          'background' : ' pink'
        }
      }
    }
  },
  methods: {                  //in a method, you need to add this. in front of your method
    clearMessage() {
      this.message = ''       //the methods can be assigned to javascript events such as keyup or mouseleave/enter values as it can be seen above
    },                        //v-show makes it so that if the length of the message is bigger than zero, the border grey value will be displayed, if it is zero, it will not be displayed
    alertMessage() {          //the difference between v-show vs v-if is that when text length is zero, v-show still has its element but doesn't display it, however v-if discards the element, does not use it
      alert(this.message)     //alert method gives you a website message, in this case it will display what is in the input field
    }
  },
  directives: {
    autofocus: {
      inserted(el) {
        el.focus()
      }
    }
  },                          //refs are not that usable when it comes to reactive data though
  mounted() {                 //we will use a ref in the lifecycle mounted instead of writing them manually as it can be seen below
   console.log(this.$refs)
   this.$refs.messageInput.className = '' //with this we can give the messageInput class any feature we want, in this case a green background
  }                                                //right now the green background is overwriting the error class's pink background feature
  //unmounted() {             normally this is how we use lifecycles
  //  console.log('unmounted');
  //}
}
</script>

<style>
  .border-grey{
    border: 1px solid grey;
  }
  input, button {
    font-size: 23px;
  }
  .error{
    color: red;
    background: pink;
  }
</style>
