<template>
  <div class="purpose">
    <form v-if="!showFeed">
      <div class="login" v-if="reason === 'Login'">
        <h4>{{ reason }}</h4>
        <div>
          <strong>
            <label
              style="font-family: Arial, Helvetica, sans-serif; font-size: 14px"
              >User Name</label
            ></strong
          >
          <input
            v-text="username"
            type="text"
            id="usrname"
            ref="username"
            :placeholder="username"
            v-model="userName"
            v-on:focus="clear"
          />
        </div>
        <br />
        <div>
          <strong>
            <label
              v-bind:title="password"
              style="font-family: Arial, Helvetica, sans-serif; font-size: 14px"
              >Password</label
            ></strong
          >
          <input
            v-text="password"
            type="password"
            id="pswrd"
            :placeholder="password"
            v-bind:title="password"
            v-model="dataIn"
          />
        </div>
        <br />
        <button
          id="login"
          type="button"
          v-on:click="allowLoginWithValidation"
          :disabled="toDisable"
        >
          Login
        </button>
        <div
          v-if="buttonClicked"
          style="
            font-family: Arial, Helvetica, sans-serif;
            font-size: 14px;
            margin-top: 8px;
          "
        >
          <span v-if="isValid">{{ errorMessage }}</span>
          <span v-else>Error : {{ errorMessage }}</span>
        </div>
      </div>
      <div
        class="other"
        style="
          font-family: Arial, Helvetica, sans-serif;
          font-size: 14px;
          margin-top: 8px;
        "
        v-else
      >
        <h3>Coming soon...</h3>
      </div>
    </form>
    <div v-else>
      <render-feed :user="userName"></render-feed>
      <div class="logout">
        <button id="logout" type="button" v-on:click="logout">Logout</button>
      </div>
    </div>
  </div>
</template>

<script>
import RenderFeed from "./RenderFeed.vue";
export default {
  name: "Login",
  props: {
    reason: String,
    toDisable: Boolean,
  },
  components: {
    RenderFeed,
  },
  data: () => ({
    username: "Type your name",
    password: "minimum 8 characters",
    dataIn: "",
    buttonClicked: false,
    isValid: true,
    errorMessage: "",
    showFeed: false,
    userName: "",
  }),
  created() {
    this.userName = "";
    this.dataIn = "";
  },
  methods: {
    allowLoginWithValidation() {
      this.buttonClicked = false;
      const usr = this.$refs.username.value;
      if (usr.length < 5) {
        this.isValid = false;
        this.errorMessage = "User Name- Need aleast 5 character";
      } else if (this.isValid && this.dataIn.length < 8) {
        this.dataIn = "";
        this.isValid = false;
        this.errorMessage = "Password- Need atleast 8 character";
      } else {
        this.isValid = true;
      }
      if (this.isValid) {
        this.errorMessage = "Login success";
        this.showFeed = true;
        this.userName = usr;
      }
      this.buttonClicked = true;
    },

    clear() {
      this.dataIn = "";
    },

    logout() {
      this.showFeed = false;
      this.errorMessage = "";
      this.userName = "";
      this.dataIn = "";
    },
  },
};
</script>

<style scoped>
h4 {
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
  margin-right: 30px;
  margin-bottom: 40px;
}

h3 {
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
}

label {
  float: left;
}

.login {
  text-align: center;
  width: 110%;
}

#usrname,
#pswrd {
  width: 65%;
}

#usrname {
  margin-left: 2px;
}

#pswrd {
  margin-left: 9px;
}

#login {
  margin-top: 8px;
  margin-right: 24px;
  border-radius: 4px;
  width: 70px;
  height: 30px;
  background-color: darkgrey;
}

.purpose {
  display: grid;
  background-color: rgb(226, 239, 247);
  height: 250px;
  padding: 50px;
  position: absolute;
  left: 37%;
  box-shadow: 5px 10px 8px #888888;
  border: 2px solid rgb(226, 239, 247);
}

#logout {
  margin-top: 8px;
  border-radius: 4px;
  width: 75px;
  height: 30px;
  background-color: darkgrey;
}

.logout {
  float: right;
}
</style>
