<template>
  <CDropdown
    inNav
    class="c-header-nav-items"
    placement="bottom-end"
    add-menu-classes="pt-0"
  >
    <template #toggler>
      <CHeaderNavItem class="d-md-down-none mx-2">
        <CHeaderNavLink>
          <CIcon name="cil-bell" />
            <div v-if=" countNoti !== 0 ">
              <span
                class="badge badge-pill badge-danger"
                >
                {{ countNoti }}
              </span>
            </div>
            <div v-if=" countNoti === 0 ">
              
            </div>
        </CHeaderNavLink>
      </CHeaderNavItem>
    </template>
      <div class="w">
        <NotiDetail/>
      </div>
  </CDropdown>
</template>

<script>

import NotiDetail from './Notidetail'
import axios from 'axios'
import io from 'socket.io-client'

export default {
  name: "TheNotification",
  data() {
    return {
      itemsCount: 42,
      countNoti : 0,
        socket: io("http://localhost:3003")
    };
  },
  components : {
      NotiDetail
  },
  created () {
    axios.get("http://localhost:3000/addnoti").then(res => {
      this.countNoti = res.data.data.length
    }),
    this.socket.on('data', (data) => {
      const id = JSON.parse(localStorage.getItem('id'))
      axios.get(`http://localhost:3000/getuserbyid/${id}`).then((res) => {
        if ( res.data.data[0].isActive === 1 && data.message === 'success') {
          axios.get("http://localhost:3000/addnoti").then(res => {
              this.noti = res.data.data
              this.countNoti = res.data.data.length
          })
        }
      })
    })
  }
};
</script>

<style scoped>
.c-icon {
  margin-right: 0.3rem;
}

</style>