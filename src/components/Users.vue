<template>
  <div class="users">
    <h1>Users getting used</h1>
    <form v-on:submit="addUser">
      <input type="text" v-model="newUser.name" placeholder="Enter name">
      <br>
      <input type="text" v-model="newUser.email" placeholder="Enter email">
      <br>
      <input type="submit" value="Submit">
    </form>
    <ul>
      <li v-for="user in users">
        <input type="checkbox" class="toggle" v-model="user.contacted">
        <span :class="{contacted: user.contacted}">{{user.name}} : {{user.email}}</span>
        <button v-on:click="deleteUser(user)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'users',
    data () {
      return {
        users: [

        ],
        newUser: {}
      }
    },
    methods: {
      addUser: function (e) {
        e.preventDefault()
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        })
      },
      deleteUser: function (user) {
        this.users.splice(this.users.indexOf(user), 1)
      }
    },
    created: function () {
      this.$http.get('http://jsonplaceholder.typicode.com/users')
        .then(function (response) {
          this.users = response.data.map(function (user) { user.contacted = false; return user })
        })
    }
  }
</script>

<style scoped>
  .contacted {
    text-decoration: line-through;
  }
</style>
