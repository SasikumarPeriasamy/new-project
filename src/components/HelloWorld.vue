<template>
  <div class="hello">
    <h3>Welocme!</h3>
    <h4>
      <span v-html="timeset"></span>
      <span style="color:red"> {{ isTimeout ? "timeout" : timeout }} </span>
    </h4>
    <Login v-bind:[checkpw]="purpose" :toDisable="isTimeout"></Login>
  </div>
</template>

<script>
import Login from "./Login.vue";
export default {
  data: () => ({
    purpose: "Login",
    timeout: 5000,
    timeset: "<span  style='color:'>Time left : </span>",
    checkpw: "reason",
    isTimeout: false,
    chanse: true,
  }),
  name: "HelloWorld",
  components: {
    Login,
  },
  props: {
    msg: String,
  },
  mounted() {
    setInterval(() => {
      this.timeout--;
      if (this.timeout === 0) {
        this.isTimeout = true;
      }
    }, 1000);
  },
  watch: {
    timeout(newTimeout) {
      if (newTimeout === 0 && this.chanse) {
        this.chanse = false;
        const result = confirm("need to reset ?");
        if (result) {
          this.timeout = 500;
          this.isTimeout = false;
        }
      }
    },
  },
};
//const take = "Sample text check";
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  text-align: center;
  margin-top: 5%;
  font-style: bold;
  font-size: 30px;
  font-family: Arial, Helvetica, sans-serif;
}

h4 {
  text-align: right;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
