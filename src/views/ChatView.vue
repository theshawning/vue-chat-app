<template>
  <div class="chatView">
    <Chat :name='name' />
  </div>
</template>

<script>
import Chat from '@/components/Chat.vue'

export default {
  name: 'ChatView',
  props: ['name'],
  components: {
    Chat
  }
}
</script>
