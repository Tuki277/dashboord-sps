<template>
  <a class="dropdown-item" href="#">
    <div class="message overflow">
      <div class="py-3 mfe-3 float-left">
        <div class="c-avatar">
          <img
            class="c-avatar-img"
            src="img/avatars/7.jpg"
            alt="user@email.com"
          /><span class="c-avatar-status bg-success"></span>
        </div>
      </div>
      <div>
        <small class="text-muted">{{ noti.name }}</small
        ><small class="text-muted float-right mt-1">Just now</small>
      </div>
      <div class="text-truncate font-weight-bold">
        <span class="text-danger">!</span> 
        <span>
          {{ noti.title }}
        </span>
      </div>
      <div class="small text-muted text-truncate">
        {{ noti.content }}
      </div>
    </div>
  </a>
</template>

<script>
export default {
  props: ["noti"],
};
</script>

<style>
.overflow {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  width: 400px;
}
</style>