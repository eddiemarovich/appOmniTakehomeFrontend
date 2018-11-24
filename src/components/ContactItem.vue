<template>
  <li class="contact">
    <span class="contact__name">{{ contactName }}</span>
    <img class="contact__chevron" src="../assets/chevron-right.png"/>
  </li>
</template>

<script>


export default {
  name: 'Contact',
  props: {
    contactName: String,
    isSelected: false,
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

  .contact__name {
    font-size: 24px;
  }

  .contact:nth-of-type(2n) {
    background-color: #F4F4F4;
  }

</style>
