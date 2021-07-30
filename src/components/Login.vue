<template>
  <img class="logo" src="../assets/logo.png" />
  <h1>Log-in</h1>
  <div class="login">
    <input type="text" v-model="email" placeholder="Enter email" />
    <input type="password" v-model="password" placeholder="Enter password" />
    <button v-on:click="login">Login</button>
  </div>
  <router-link to="/sign-up"></router-link>
</template>
<script>
import axios from "axios";
export default {
  name: "LogIn",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async login() {
      const result = await axios.post("http://localhost:3000/users", {
        email: this.email,
        password: this.password,
      });
      if(result.status === 201){
      localStorage.setItem("user-info", JSON.stringify(result.data))
      this.$router.push({name:'Home'})
      }

    },
  },
  mounted(){
   let user = localStorage.getItem("user-info")   
   if(user){
      this.$router.push({name:'Home'})   
   }
  }
};
</script>
<style scoped>
.logo {
  width: "100px";
}
.login input {
  width: 300px;
  height: 25px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid skyblue;
}
.login button {
  height: 30px;
  width: 320px;
  color: white;
  background: skyblue;
  border: 1px solid skyblue;
  cursor: pointer;
}
</style>

