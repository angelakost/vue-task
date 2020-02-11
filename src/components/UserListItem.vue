<template>
  <li>
    <article class="user">
      <button class="user__trigger" v-on:click="isActive = !isActive" v-on:blur="isActive = false">
        <div class="user__image">
          <img v-bind:src="user.img"  alt="">
        </div>
        <div class="user__info">
          <h2>{{user.firstname}} {{user.lastname}}</h2>
          <p class="user__age"  v-bind:class="{ showInfo: isActive}">
            Age: {{user.age}}
          </p>
        </div>
      </button>
      <div class="user__extra-info">
      </div>
    </article>
  </li>
</template>

<script>
    export default {
      name: "UserListItem",
      data(){
        return{
          isActive: false
        }
      },
      props:{
        user: Object,
      }
    }
</script>

<style scoped>
</style>
