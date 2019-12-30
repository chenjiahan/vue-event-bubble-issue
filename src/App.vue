<template>
  <div id="app">
    <div ref="parent" class="parent" @click="onClickParent">
      Parent
      <div ref="child" class="child" @click="onClickChild">Child</div>
    </div>

    <ul>
      <li v-for="(event, index) in events" :key="index">{{ event }}</li>
    </ul>
  </div>
</template>

<script>
/* eslint-disable no-console */
export default {
  name: 'App',
  data() {
    return {
      events: []
    };
  },
  mounted() {
    const ua = navigator.userAgent;
    this.events.push('UserAgent' + ua);

    this.$refs.parent.addEventListener('click', this.onNativeClickParent);
    this.$refs.child.addEventListener('click', this.onNativeClickChild);
  },
  methods: {
    onClickParent() {
      console.log('parent clicked');
      this.events.push('parent clicked');
    },
    onClickChild() {
      console.log('child clicked');
      this.events.push('child clicked');
    },
    onNativeClickParent(event) {
      const msg = 'native child clicked: event.timeStamp: ' + event.timeStamp;
      const msg2 = 'native parent clicked: Date.now: ' + Date.now();

      console.log(msg);
      console.log(msg2);

      this.events.push(msg);
      this.events.push(msg2);
    },
    onNativeClickChild(event) {
      const msg = 'native child clicked: event.timeStamp: ' + event.timeStamp;
      const msg2 = 'native child clicked: Date.now: ' + Date.now();

      console.log(msg);
      console.log(msg2);

      this.events.push(msg);
      this.events.push(msg2);
    }
  }
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.parent {
  width: 300px;
  height: 300px;
  background-color: red;
}

.child {
  width: 100px;
  height: 100px;
  background-color: blue;
}

li {
  text-align: left;
}
</style>
