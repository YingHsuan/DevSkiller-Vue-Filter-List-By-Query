<template>
  <div id="app">
    <!-- Two way bind query to this input field -->
    <input id="search" type="text" v-model="query">
    <!--
      Edit app-contacts component to receive
      contacts property through search results
    -->
    <app-contacts :contacts="search"></app-contacts>
  </div>
</template>

<script>
import Contacts from './components/Contacts'
/**
 * To import contact from contacts.json
 * uncomment the following line
 */
import jsonContacts from './assets/contacts.json'

export default {
  name: 'App',
  components: {
    'app-contacts': Contacts
  },
  data () {
    /**
     * Create the necessary data variable here
     */
    return {
      query: '',
      Contacts: jsonContacts
    }
  },
  computed: {
    search: {
      /**
       * Complete this function to
       * search through contacts
       * by first and last name, email & phone number
       * and return an array with the results
       */
      get: function () {
        var query = this.query
        if (query && query.length > 0) {
          var filterContract = []
          this.Contacts.forEach(item => {
            var isBingo = false
            if (item.firstname.includes(query) ||
              item.lastname.includes(query)
            ) {
              isBingo = true
            } else {
              item.email.forEach(_email => {
                if (_email.includes(query)) {
                  isBingo = true
                }
              })
              item.phoneNumber.forEach(_phoneNumber => {
                if (_phoneNumber.includes(query)) {
                  isBingo = true
                }
              })
            }
            if (isBingo) {
              filterContract.push(item)
            }
          })
          return filterContract
        } else {
          return this.Contacts
        }
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
