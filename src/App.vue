<template>
  <div id="app">
    <Header msg="One contact list to rule them all..."/>
    <div class="main-container">
      <Sidebar
        v-on:selectContact='updateSelectedContact'
        :selectedContactId='selectedContact ? selectedContact.id : null'
        :contacts='contacts'
      />
      <NewContactForm
        :contactIsSelected='selectedContact !== null'
        v-on:postNewContact='onUpdateFetch'
      />
      <ContactDetails
        v-on:deSelectContact='updateSelectedContact'
        :selectedContact='selectedContact'
        :deleteContact='deleteContact'
      />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Sidebar from './components/Sidebar.vue'
import DetailsView from './components/Details/DetailsView.vue'
import NewContactForm from './components/Details/NewContactForm.vue'
import ContactDetails from './components/Details/ContactDetails.vue'


export default {
  name: 'app',
  data: function() {
    return {
      selectedContact: null,
      contacts: [],
      shouldFetch: false
    }
  },
  components: {
    Header,
    Sidebar,
    DetailsView,
    NewContactForm,
    ContactDetails
  },
  methods: {
    fetchContacts: async function() {
      const contactsRequest = await fetch(`http://localhost:8000/api/contacts`)
      const contactsJson = await contactsRequest.json()

      this.contacts = contactsJson
      this.contacts.sort((a, b) => {
        let textA = a.title.toUpperCase()
        let textB = b.title.toUpperCase()
        return (textA < textB) ? -1 : (textA > textB) ? 1 : 0
      })
    },
    deleteContact: async function(id) {
      const myHeaders = new Headers()
      myHeaders.append('Content-Type', 'application/json; charset=utf-8')
      myHeaders.append('access-control-allow-origin', '*')

      const deleteFetch = await fetch(`http://localhost:8000/api/contacts/${id}`, {
        method: 'DELETE',
        headers: myHeaders
      })
      this.fetchContacts()
    },
    updateSelectedContact: function(value) {
      this.fetchContacts()
      this.selectedContact = value
    },
    onUpdateFetch: function() {
      this.fetchContacts()
    }
  },
  mounted() {
    this.fetchContacts()
  },
}
</script>

<style>
  body {
    margin: 0px;
    font-family: "Lato";
    font-weight: lighter;
    text-overflow: clip;
  }

  div {
    padding: 0px;
  }

  .app {
    padding: 0px;
  }

  .main-container {
    display: flex;
    flex-direction: row;
  }
</style>
