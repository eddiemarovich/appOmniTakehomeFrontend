<template>
  <div class="details-container">
    <NewContactForm :selectedContactId="this.selectedContactId"/>
  </div>
</template>

<script>
import NewContactForm from './NewContactForm.vue'

export default {
  name: 'DetailsView',
  data: function() {
    return {
      showDetails: false
    }
  },
  props: {
    selectedContactId: Number
  },
  components: {
    NewContactForm
  }
}

</script>

<style>


</style>
