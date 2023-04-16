<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <br />
    <input
      placeholder="Enter your string"
      v-model.lazy="message"
      @keyup.enter="addItem"
    />
    <button type="button" class="btn btn-success" v-on:click="handleClick">
      <i class="fas fa-search"></i>
    </button>
    <br />
    <div v-if="hasSlash" class="list">
      <ul>
        <li v-for="item in message" :key="item">
          {{ item }}
        </li>
      </ul>
    </div>
    <div v-else>
      <p class="item-left">You typed: {{ message }}</p>
    </div>
    <br />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data() {
    return {
      message: '',
      items: [],
    };
  },
  components: {
    HelloWorld,
  },
  methods: {
    handleClick() {
      console.log("Input value:", this.message);
    },
  },
  computed: {
    hasSlash() {
      return /\//.test(this.message);
    },
  },
  watch: {
    message() {
      if (this.hasSlash) {
        this.items = this.message.split('/').reduce((acc, curr) => {
          const letters = curr.split('').filter(char => char !== '/');
          return [...acc, ...letters];
        }, []);
      } else {
        this.items = [this.message];
      }
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
input {
  border-radius: 5px;
  border: 2px solid blue;
  margin-right: 10px !important;
  height: 38px;
}
.bind-button {
  border: 2px solid lightsalmon;
  width: 500px;
  height: 300px;
  margin-left: 32%;
}
.item-left {
  font-size: x-large;
  font-weight: bold;
  margin-right: 400px;
  margin-top: 5px;
}
ul {
  display: flex;
  flex-direction: column;
  align-items: center;
  list-style-type: square;
  margin-left: 30px;
  margin-top: 5px;
  font-size: x-large;
  font-weight: bold;
}
.list {
  margin-left: 40%;
  margin-top: 5px;
  font-size: x-large;
  font-weight: bold;
  border: 3px solid lightsalmon;
  width: 300px;
  height: 500px;
}
</style>
