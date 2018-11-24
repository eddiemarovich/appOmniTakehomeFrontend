<template>
  <div class="details-container">
    <NewContactForm />
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
    selectedContact: null
  },
  components: {
    NewContactForm
  }
}

</script>

<style>


</style>
