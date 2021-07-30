<template>
  <img class="logo" src="../assets/logo.png" />
  <h1>Sign Up</h1>
  <div class="register">
    <input type="text" v-model="name" placeholder="Enter name" />
    <input type="text" v-model="email" placeholder="Enter email" />
    <input type="password" v-model="password" placeholder="Enter password" />
    <button v-on:click="signUp">Sign Up</button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  methods: {
    async signUp() {
      const result = await axios.post("http://localhost:3000/users", {
        email: this.email,
        name: this.name,
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
.register input {
  width: 300px;
  height: 25px;
  display: block;
  margin-left: auto;
  margin-right: auto;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid skyblue;
}
.register button {
  height: 30px;
  width: 320px;
  color: white;
  background: skyblue;
  border: 1px solid skyblue;
  cursor: pointer;
}
</style>

