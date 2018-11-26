<template>
  <div class="details-container">
    <NewContactForm :contactIsSelected='selectedContact !== null' />
    <ContactDetails :selectedContact='selectedContact' />
  </div>
</template>

<script>
import NewContactForm from './NewContactForm.vue'
import ContactDetails from './ContactDetails.vue'

export default {
  name: 'DetailsView',
  data: function() {
    return {
      showDetails: false
    }
  },
  props: {
    selectedContact: Object | null
  },
  components: {
    NewContactForm,
    ContactDetails
  }
}

</script>

<style>


</style>
