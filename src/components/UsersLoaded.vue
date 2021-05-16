<template>
  <div class="users-loaded">
    <span class="users-loaded__text">All users loaded</span>
  </div>
</template>

<script>
export default {
  name: "UsersLoaded"
}
</script>

<style scoped>
  .users-loaded {
    background: #EDF9F2;
    border-radius: 67px;
    text-align: center;
    padding: 26px 0;
  }

  .users-loaded__text {
    font-size: 20px;
    line-height: 20px;
    color: #219653;
  }

  .users-loaded__text::before {
    content: '';
    display: inline-block;
    width: 18px;
    height: 15px;
    margin-right: 13px;
    background-image: url("../assets/icons/checkmark.svg");
  }
</style>
