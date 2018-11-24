<template>
  <form class="c-form" id="signin">
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
let users = [];
base("Users").select({
    // Selecting the first 3 records in Grid view:
    maxRecords: 3,
    view: "Grid view"
  }).eachPage(function page(records, fetchNextPage) {
      // This function (`page`) will get called for each page of records.
      records.forEach(function(record) {
        users.push(record);
        // If there are no more records, `done` will get called.
      });

      // To fetch the next page of records, call `fetchNextPage`.
      // If there are more records, `page` will get called again.
      fetchNextPage();
    },
    function done(err) {
      if (err) {
        console.error(err);
        return;
      }
    }
  );
// @ is an alias to /src
import Input from "@/components/Input.vue";

export default {
  name: "Signin",
  data() {
    return {
      atUsers: [],
      email: "",
      password: ""
    };
  },
  $mounted: function() {
    this.getUsers(users);
  },
  components: {
    Input
  },
  methods: {
    getUsers: function(users) {
      this.data.atUsers = users;
      console.log(this.data.atUsers);
    },
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
