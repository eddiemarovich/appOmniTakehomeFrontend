<template>
  <li v-on:click="" class="contact">
    <span class="contact__name">{{ contactName }}</span>
    <img class="contact__chevron" src="../assets/chevron-right.png"/>
  </li>
</template>

<script>
export default {
  name: 'Contact',
  props: {
    contactName: String,
    isSelected: Boolean,    
  },
  data: function() {
    return {
      isFavorite: null
    }
  },
}

</script>

<style scoped>
  li {
    padding-left: 10px;
    padding-right: 10px;
    display: flex;
    justify-content: space-between;
  }

  .contact__chevron {
    height: 28px;
  }

  .contact {
    width: 100%;
    height: 50px;
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  .contact:nth-of-type(2n) {
    background-color: #F4F4F4;
  }

  .contact:hover {
    background-color: #707070;
  }

  .contact__name {
    font-size: 24px;
  }

</style>
