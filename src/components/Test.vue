<template>
  <div class="test">
    <input type="text" v-model="title"><br/>
    <h1>{{title}}</h1>
    <p v-if="showName">{{user.firstName}}, your last name is {{user.lastName}}</p>
    <p v-else>Nobody is here.</p>
    <ul>
      <li v-for="item in items">{{item.title}}</li>
    </ul>
    <button v-on:click="greet('Hello World')">Say Greeting</button>
    <input type="text" v-on:keyup="pressKey" v-on:keyup.enter="enterHit">
    <hr/>
    <label>First Name: </label><input type="text" v-model="user.firstName"><br>
    <label>Last Name: </label><input type="text" v-model="user.lastName"><br>
    <h3>{{fullName}}</h3>
    <h2>{{msg}}</h2>
  </div>
</template>

<script>
  export default {
    name: 'test',
    props: {
      msg: {
        type: String,
        default: 'Foobar'
      }
    },
    data () {
      return {
        title: 'This is a test of the emergency broadcast system!',
        user: {
          firstName: 'John',
          lastName: 'Doe'
        },
        showName: true,
        items: [
          {title: 'Item 1'},
          {title: 'Item 2'},
          {title: 'Item 3'}
        ]
      }
    },
    methods: {
      greet: (greeting) => alert(greeting),
      pressKey: (ev) => console.log(`${ev.key} pressed!`),
      enterHit: () => console.log('HIT')
    },
    computed: {
      fullName: function () { return `${this.user.firstName} ${this.user.lastName}` }
    }
  }
</script>

<style scoped>

</style>
