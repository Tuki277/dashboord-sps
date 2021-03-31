<template>
  <div>
    <div class="dropdown-header bg-light">
      <strong>You have {{ count }} messages</strong>
    </div>
    <Notitab 
        :key="noti.id"
        :noti="noti"
        v-for="noti in noti"
        :count="count"
      />
    <a class="dropdown-item text-center border-top" href="#">
      <strong>View all messages</strong>
    </a>
  </div>
</template>



<script>
import Notitab from "./Notitab";
import axios from "axios";
import io from 'socket.io-client'

export default {
  components: {
    Notitab,
  },
  created() {
    axios.get("http://localhost:3000/addnoti").then((res) => {
      this.noti = res.data.data;
      this.count = res.data.data.length;
    }),
    this.socket.on('data', data => {
      console.log({ data })
      if ( data.message === 'success') {
        axios.get("http://localhost:3000/addnoti").then((res) => {
          this.noti = res.data.data;
          this.count = res.data.data.length;
        })
      }
    })
  },
  data() {
    return {
      noti: [],
      count: 0,
      socket: io("http://localhost:3003")
    };
  },
};
</script>

<style>
</style>