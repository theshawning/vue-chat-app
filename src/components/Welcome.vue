<template>
  <div class="welcome container">
    <div class="card">
      <div class="card-content center-align">
        <h2 class="teal-text">Welcome</h2>
        <form @submit.prevent='enterChat'>
          <label for="name">Enter your name:</label>
          <input type="text" name="name" v-model="name">
          <p v-if="feedback" class="red-text">{{ feedback }}</p>
          <button class="btn teal">Enter Chat</button>
        </form>
      </div>
    </div>    
  </div>
</template>

<script>
export default {
  name: 'Welcome',
  data(){
    return {
      name: null,
      feedback: null
    }
  },
  methods: {
    enterChat(){
      if(this.name){
        this.$router.push({ name: 'Chat', params: { name: this.name } })
      } else {
        this.feedback = 'You must enter a name to join chat.'
      }
    }
  }
}
</script>

<style lang="scss">
.welcome {
  max-width: 500px;
  margin-top: 100px;

  & h2 {
    font-size: 3rem;
  }

  & button {
    margin: 30px auto 20px;
  }
}
label {
  font-size: 1rem;
}
</style>
