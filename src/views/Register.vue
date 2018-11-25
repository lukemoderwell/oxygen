<template>
  <form class="c-form" id="register">
    <Input 
      v-model="user.firstName"
      type="text" 
      placeholder="John" 
      label="First Name" />
    <Input 
      v-model="user.lastName"
      type="text" 
      placeholder="Doe" 
      label="Last Name" />
    <Input 
      v-model="user.email"
      type="email" 
      placeholder="me@name.com" 
      label="Email" />
    <Input 
      v-model="user.password" 
      type="password" 
      label="Password" 
      v-bind:minlength="4" />
    <Input 
      v-model="user.confirmPassword" 
      type="password" 
      label="Confirm Password" 
      v-bind:minlength="4" />
    <input type="submit" v-on:click="handleSubmit"/>
  </form>
</template>

<script>
import Airtable from "airtable";
Airtable.configure({
  endpointUrl: "https://api.airtable.com",
  apiKey: process.env.VUE_APP_AT_API_KEY
});
const base = Airtable.base(process.env.VUE_APP_AT_BASE);
// @ is an alias to /src
import Input from "@/components/Input.vue";

export default {
  name: "Register",
  data() {
    return {
      user: {
        firstName: "",
        lastName: "",
        email: "",
        image: "",
        password: "",
        confirmPassword: ""
      }
    };
  },
  components: {
    Input
  },
  methods: {
    handleSubmit: function(event) {
      event.preventDefault();
      this.createUser(this.user);
    },
    checkPassword: function(password, confirm) {
      let result = false;
      if (password !== '') {
        password == confirm 
          ?  result = true : result = false
      }
      return result;
    },
    formError: function(user) {
      let errors = [];
      for (var key in user) {
        user[key] == '' ? errors.push(key) : '';
      }
      alert(String(errors));
    },
    createUser: function(data) {
      if (this.checkPassword(data.password, data.confirmPassword)) {
        base("Users").create({
          email: data.email,
          firstName: data.firstName,
          lastName: data.lastName,
          image: [
            {
              url: "https://dl.airtable.com/hyJetILvQ22MlnH5PsYN_luke.jpg"
            }
          ],
          password: data.password
        },
        function(err, record) {
          if (err) {
            console.error(err);
            return;
          }
          console.log(record.getId());
        });
      } else {
        this.formError(this.user);
      }
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
