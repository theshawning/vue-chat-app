<template>
  <div class="chat container">
    <h2 class="center teal-text">Vue Chat</h2>
    <div class="card">
      <div class="card-content">
        <ul class="messages" v-chat-scroll>
          <li v-for="message in messages" :key='message.id'>
            <span class="teal-text">{{ message.name }} </span>
            <span class="grey-text text-darken-3">{{ message.content }}</span>
            <span class="grey-text time">{{ message.timestamp }}</span>
          </li>
        </ul>
      </div>
      <div class="card-action">
        <NewMessage :name="name" />
      </div>
    </div>
  </div>
</template>

<script>
import NewMessage from '@/components/NewMessage.vue'
import db from '../firebase/init'
import moment from 'moment'

export default {
  name: 'Chat',
  props: ['name'],
  components: {
    NewMessage
  },
  data() {
    return {
      messages: []
    }
  },
  created(){
    let ref = db.collection('messages').orderBy('timestamp')
    ref.onSnapshot(snapshot => {
      snapshot.docChanges().forEach(change => {
        if(change.type == 'added'){
          let doc = change.doc
          this.messages.push({
            id: doc.id,
            name: doc.data().name,
            content: doc.data().content,
            timestamp: moment(doc.data().timestamp).format('lll')
          })
        }
      })
    })
  }
}
</script>

<style lang="scss">
.chat {
  & h2 {
    font-size: 2.6rem;
    margin-bottom: 40px;
  }

  & span {
    font-size: 1.4em;
  }

  & .time {
    display: block;
    font-size: 1rem;
  }
}
.messages {
  max-height: 300px;
  overflow: auto;

  &::-webkit-scrollbar {
    width: 8px;

    &-track {
      background: #ddd;
    }

    &-thumb {
      background: #aaa;
    }
  }
}
</style>