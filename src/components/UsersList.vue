<template>
  <div class="user-list">
<!--    <p>Active user is {{activeUser}}</p>-->
    <transition name="vlez">
      <slot v-if="!users.length"></slot>
    </transition>

    <transition name="vlez">
      <div v-if="users.length">
        <h3 class="results-message">{{users.length}} users found</h3>
        <ul>
          <user-item v-for="user in users" :key="user.id" :user="user"></user-item>
        </ul>
      </div>
    </transition>

  </div>
</template>

<script>
    import UserListItem from "./UserListItem";

    export default {
      name: "UserList",
      components:{
        'user-item': UserListItem
      },
      props:{
          users: Array
      }
    }
</script>

<style lang="scss">
  .vlez-enter-active, .vlez-leave-active {
    transition: all 1s;
  }
  .vlez-enter, .vlez-leave-to {
    transform: translateY(50px);
    filter: blur(10px);
    opacity: 0;
  }

ul{
  padding: 0;
  margin: 0;
}

.user-list{
  padding: 20px;
  border: 1px solid #aaa;
}

.results-message{
  margin: 5px 0px 20px 0px;
}
</style>
