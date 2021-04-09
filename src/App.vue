<template>
  <router-view></router-view>
</template>

<script>

import io from 'socket.io-client'

export default {
  name: 'App',
  data () {
    return {
      socket: io("http://localhost:3003")
    }
  },
  created () {
    this.socket.on('update', data => {
      console.log(data);
      if (data.id === localStorage.getItem('id')) {
        if (data.message === 'updated') {
          this.logout()
        }
      }
    })
  },
  methods: {
    logout () {
      alert("dang nhap lai de thay doi phan quyen")
      localStorage.removeItem('id')
      localStorage.removeItem('Token')
      this.$router.push('/pages/login')
    }
  }
}
</script>

<style lang="scss">
  // Import Main styles for this application
  @import 'assets/scss/style';
</style>