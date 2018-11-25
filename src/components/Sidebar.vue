<template>
  <div class="sidebar">
    <div class="sidebar__title">
      <span>Contacts</span>
    </div>
    <ul>
      <ContactItem v-for="contact in contacts" :contactName="contact"/>
    </ul>
  </div>
</template>

<script>
import ContactItem from './ContactItem.vue'

export default {
    name:'Sidebar',
    props: {
      title: String,
    },
    data: function() {
      return {
        contacts: []
      }
    },
    components: {
      ContactItem
    },
    methods: {
      fetchContacts: async function() {
        const contactsRequest = await fetch(`http://localhost:8000/api/contacts`)
        const contactsJson = await contactsRequest.json()

        this.contacts = contactsJson.map(contact => {
          return contact.title
        }).sort()

      }
    },
    mounted() {
      this.fetchContacts()
    }
  }
</script>

<style scoped>
  h4 {
    margin: 0px;
  }

  ul {
    margin: 0px;
    padding: 0px;
    list-style-type: none;

  }

  .sidebar__title {
    border-bottom: solid 1px #707070;
    height: 15%;
    display: flex;
    padding-left: 8px;
    align-items: center;
    font-size: 32px;
  }

  .sidebar {
    width: 25vw;
    border-right: solid 1px #707070;
    height: 85vh;
    position: fixed;
    top: 15vh;
    bottom: 0;
    overflow: scroll;
  }
</style>
