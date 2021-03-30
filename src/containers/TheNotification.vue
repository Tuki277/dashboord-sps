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
          <span class="badge badge-pill badge-danger">4</span>
        </CHeaderNavLink>
      </CHeaderNavItem>
    </template>

    <NotiDetail/>

  </CDropdown>
</template>

<script>
import axios from "axios";
import NotiDetail from './Notidetail'

export default {
  name: "TheNotification",
  data() {
    return {
      noti : [],
      itemsCount: 42,
    };
  },
  components : {
      NotiDetail
  },
  created () {
    axios.get("http://localhost:3000/addnoti").then(res => {
        console.log(res.data.data)
        this.noti = res.data.data
    })
  }
};
</script>

<style scoped>
.c-icon {
  margin-right: 0.3rem;
}
</style>