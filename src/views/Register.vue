<template>
  <form class="c-form" id="register">
    <Input 
      v-model="firstName"
      type="text" 
      placeholder="John" 
      label="First Name" />
    <Input 
      v-model="lastName"
      type="text" 
      placeholder="Doe" 
      label="Last Name" />
    <Input 
      v-model="email"
      type="email" 
      placeholder="me@name.com" 
      label="Email" />
    <Input 
      v-model="password" 
      type="password" 
      label="Password" 
      v-bind:minlength="4" />
    <Input 
      v-model="confirmPassword" 
      type="password" 
      label="Confirm Password" 
      v-bind:minlength="4" />
    <input type="submit" v-on:click="handleSubmit"/>
    
  </form>
</template>

<script>
// @ is an alias to /src
import Input from "@/components/Input.vue";

export default {
  name: "Register",
  data() {
    return {
      firstName: '',
      lastName: '',
      email: '',
      password: '',
      confirmPassword: ''
    };
  },
  components: {
    Input
  },
  methods: {
    handleSubmit: function(event) {
      event.preventDefault();
      console.log(`email: ${this.email}, password: ${this.password}`);
    }
  }
};
</script>

<style lang="scss" scoped>
.c-form {
  max-width: 480px;
  margin: 0 auto;
}
</style>
