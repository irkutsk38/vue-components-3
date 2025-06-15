<template>
  <div class="user-card">
    <div v-if="loading">Загрузка...</div>
    <div v-else-if="error">Ошибка: {{ error }}</div>
    <div v-else-if="user">
      <img :src="user.avatar_url" width="100" style="float:left; margin-right: 10px" />
      <strong>{{ user.name || user.login }}</strong><br>
      {{ user.bio || 'Нет описания' }}<br>
      <a :href="user.html_url" target="_blank">GitHub</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UserProfile',
  props: ['username'],
  data() {
    return {
      user: null,
      loading: false,
      error: null
    }
  },
  mounted() {
    this.fetchUser()
  },
  methods: {
    async fetchUser() {
      this.loading = true
      try {
        const res = await fetch(`https://api.github.com/users/${this.username}`)
        if (!res.ok) throw new Error('User not found')
        this.user = await res.json()
        this.$emit('notify', `Профиль ${this.username} загружен`, 'success')
      } catch (err) {
        this.error = err.message
        this.$emit('notify', err.message, 'error')
      } finally {
        this.loading = false
      }
    }
  }
}
</script>

<style scoped>
.user-card {
  border: 1px solid #ccc;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 6px;
  background-color: #fdfdfd;
}
</style>
