<template>
  <div class="notification" :class="type">
    <strong>{{ type.toUpperCase() }}:</strong> {{ message }}
    <button @click="$emit('close')" style="float:right">×</button>
  </div>
</template>

<script>
export default {
  name: 'NotificationMessage',
  props: ['type', 'message']
}
</script>

<style scoped>
  .notification {
    border: 1px solid #ccc;
    padding: 10px;
    border-radius: 6px;
    margin-bottom: 15px;
  }

    .notification.success {
      background-color: #e0f8e0;
    }

    .notification.error {
      background-color: #f8e0e0;
    }
</style>
