<template>
  <div id="app">
    <section class="user-filter">
      <label for="input-field">Filter Users by Name</label>
      <input type="text" v-model="filterTerm" id="input-field" placeholder="Enter user name..."/>
      <transition name="fade">
        <span class="user-filter__no-users-found"></span>
      </transition>
      <button class="filter-button" v-on:click="sortByAge">Sort by Age (the youngest first)</button>
    </section>
    <user-list :users="filterResults">
      <div class="result-message">
        <img src="./assets/error.png" height="50" alt="Error">
        <h4 class="alert-message">No users found</h4>
      </div>
    </user-list>
  </div>
</template>

<script>
import UsersList from "./components/UsersList";
import {usersList} from "./users";

export default {
  name: 'app',
  components: {
    'user-list': UsersList,
  },

  data () {
    return {
      filterTerm: '',
      users: usersList
    }
  },

  computed: {
    filterResults: function(){
      if (this.filterTerm.length >= 3){
        return this.users.filter((user) => {
          return user.firstname.toLowerCase().includes(this.filterTerm.toLowerCase())
        });
      }
      else {
        return this.users;
      }
    }
  },

  methods: {
    //Sorting function
    sortByAge() {
      this.users.sort((a, b) => (a.age > b.age) ? 1 : -1);
    },

  },
}
</script>

<style lang="css">
  @import url('https://fonts.googleapis.com/css?family=Roboto+Condensed&display=swap');

  body {
    background: #fff;
    font-family: 'Roboto Condensed', sans-serif;
  }

  h1,h2,h3,h4,h5,p,button{
    margin: 0;
    font-family: 'Roboto Condensed', sans-serif;
  }

  label {
    font-weight: bold;
    font-size: 1.5rem;
    display: block;
  }

  .user-list {
    margin-top: 20px;
  }

  .user-list li {
    margin-bottom: 20px;
    list-style-type: none;
  }

  input {
    padding: 10px 15px;
    margin-top: 10px;
    width: 200px;
  }

  .filter-button {
    display: block;
    margin-top: 20px;
    padding: 10px 20px;
    border-radius: 20px;
    border: 0;
    background: #0080ff;
    color:#fff;
    font-weight: bold;
  }

  .user__image {
    flex-basis: 50px;
    margin-right: 10px;
    flex-shrink: 0;
    width: 50px;
    height: 50px;
    overflow: hidden;
    border-radius: 50%;
  }

  .user-image img {
    object-fit: cover;
    width: 100%;
    height: 100%;
    display: block;
  }

  .user__trigger {
    display: flex;
    width: 100%;
    align-items: center;
    background: transparent;
    border: 0;
    padding: 0;
    text-align: left;
    margin-bottom: 15px;
    cursor: pointer;
  }

  .user__age {
    font-size: 0.8rem;
    color: gray;
    font-weight: bold;
    letter-spacing: 1px;
  }

  .user-filter__no-users-found {
    display: inline-block;
    margin-left: 10px;
  }

  .user__age {
    display: none;
  }

  .showInfo {
    display: block;
  }

  .result-message{
    display: block;
    text-align: center;
  }

  .alert-message{
    color:#aa0000;
  }

</style>
