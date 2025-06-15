<template>
  <div class="app">
    <h1>Vue 3 Component Demo (Options API)</h1>
    <NotificationMessage v-if="notificationMessage"
                         :type="notificationType"
                         :message="notificationMessage"
                         @close="notificationMessage = ''" />
    <UserProfile :username="githubUser" @notify="handleNotification" />
  </div>
</template>

<script>
  import UserProfile from './components/UserProfile.vue'
  import NotificationMessage from './components/NotificationMessage.vue'

  export default {
    name: 'App',
    components: {
      UserProfile,
      NotificationMessage
    },
    data() {
      return {
        githubUser: 'octocat',
        notificationMessage: '',
        notificationType: 'success'
      }
    },
    methods: {
      handleNotification(msg, type) {
        this.notificationMessage = msg
        this.notificationType = type
      }
    }
  }
</script>

<style>
  body {
    font-family: Arial, sans-serif;
    background: #f9f9f9;
    padding: 20px;
  }

  .app {
    max-width: 800px;
    margin: auto;
    background: #fff;
    padding: 20px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
  }
</style>





