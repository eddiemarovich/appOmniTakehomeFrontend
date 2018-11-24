<template>
  <div class="header">
    <span class="header__title">
      {{ msg }}
    </span>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  }
}
</script>

<style scoped>

.header__title {
  color: #36E29F;
  margin: 0px;
  padding-left: 10px;
  font-size: 48px;
}

.header {
  background-color: #707070;
  height: 15vh;
  display: flex;
  align-items: center;
}
</style>
