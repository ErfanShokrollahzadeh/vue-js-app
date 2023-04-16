<template>
  <div class="main">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld  />
    <input type="text" v-model.lazy="inputValue" placeholder="Enter your value">
    <button type="button" class="btn btn-success" v-on:click="handleClick">
      <i class="fas fa-search"></i>
    </button>
    <br />
    <div v-if="hasSlashes">
      <ul>
        <h6>Items:</h6>
        <li v-for="item in items" :key="item">{{ item }}</li>
      </ul>
    </div>
    <div v-else>
      <p>You typed: {{ inputValue }}</p>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";


export default {
  data() {
    return {
      inputValue: '',
      items: []
    }
  },
  components: {
    HelloWorld,
  },
  computed: {
    hasSlashes() {
      return /\//.test(this.inputValue);
    }
  },
  watch: {
    inputValue() {
      if (this.hasSlashes) {
        this.items = this.inputValue.split('/').reduce((acc, curr) => {
          const letters = curr.split('').filter(char => char !== '/');
          return [...acc, ...letters];
        }, []);
      } else {
        this.items = [this.inputValue];
      }
    }
  }
}
</script>


<style>
.main {
  margin: 100px 0px 0 600px;
}
button {
  margin-left: 10px !important;
  margin-top: -3px !important;
}
input {
  width: 200px !important;
  height: 35px !important;
  border: 2px solid blue !important;
}
h6 {
  color: red;
  margin-left: -30px;
}
</style>