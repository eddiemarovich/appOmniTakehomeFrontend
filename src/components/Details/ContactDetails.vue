<template>
  <div v-if='selectedContact' class="contact-details">
    <button v-on:click='deSelectContact(null)' class="contact-details__close">x</button>
    <span class="label">Name</span>
    <div class="contact-details__top-row">
      <div class='contact-details__name-edit'>
        <input  class="contact-details__name--editable" v-model="contact.title"/>
        <div class="details-button-container">
          <button v-on:click='handleTwoFunctions(null)' class="details-button">delete</button>
        </div>
      </div>
    </div>
    <button v-on:click="putRequestName" class="button">SAVE</button>
    <div class=" details-container">
        <div class='contact-details__name-edit'>
          <input class="contact-details__name--editable" v-model="contact.contactDetails[0].number" />
          <div class="details-button-container">
          </div>
        </div>
        <div class='contact-details__name-edit'>
          <input  class="contact-details__name--editable" v-model="contact.contactDetails[0].email"/>
          <div class="details-button-container">
          </div>
        </div>
        <div class='contact-details__name-edit'>
          <input  class="contact-details__name--editable" v-model="contact.contactDetails[0].nickname"/>
          <div class="details-button-container">
          </div>
        </div>
    </div>
    <button v-on:click='putRequestDetails' class="button">SAVE</button>

  </div>
</template>

<script>
export default {
  name: 'ContactDetails',
  props: {
    selectedContact: Object,
    deleteContact: Function
  },
  data: function() {
    return {
      nameIsEditable: false,
      detailsAreEditable: false,
      contact: {name: '', contactDetails: [{number: 'none', email: 'none', nickname: 'none'}]}
    }
  },
  methods: {
    deSelectContact: function(val, bool) {
      this.$emit('deSelectContact', val, bool)
    },
    putRequestName: async function (val) {
      const myHeaders = new Headers()
      myHeaders.append('Content-Type', 'application/json; charset=utf-8')
      myHeaders.append('access-control-allow-origin', '*')

      const body = {
        title: this.contact.title
      }
      const putFetch = await fetch(`http://localhost:8000/api/contacts/${this.contact.id}`, {
        method: 'PUT',
        headers: myHeaders,
        body: JSON.stringify(body)
      })
    },
    putRequestDetails: async function() {
      const myHeaders = new Headers()
      myHeaders.append('Content-Type', 'application/json; charset=utf-8')
      myHeaders.append('access-control-allow-origin', '*')

      const body = {
        number: this.contact.contactDetails[0].number,
        email: this.contact.contactDetails[0].email,
        nickname: this.contact.contactDetails[0].nickname
      }

      const putFetch = await fetch(`http://localhost:8000/api/contacts/${this.contact.id}/details/${this.contact.contactDetails[0].id}`, {
        method: 'PUT',
        headers: myHeaders,
        body: JSON.stringify(body)
      })
    },
    handleTwoFunctions: function(val) {
      this.deleteContact(this.selectedContact.id)
      this.deSelectContact(val)
    }
  },
  updated() {
    this.contact = this.selectedContact
  }
}

</script>


<style>
  .label {
    font-size: 36px;
    margin-bottom: -20px;
  }

  .details-container {
    display: flex;
    flex-direction: column;
    height:
  }

  .contact-details {
    width: 75vw;
    margin-left: 25vw;
    padding-left: 35px;
    padding-right: 35px;
    padding-top: 15px;
  }

  .contact-details__top-row {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }

  .contact-details__name-edit {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 50%;
    margin-bottom: 10px;
  }

  .contact-details__name {
    font-size: 42px;
    width: 90%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .contact-details__name--editable {
    border: 1px solid  #707070;
    font-size: 28px;
    margin-right: 10px;
    width: 70%;
    padding: 5px;
  }

  .contact-details__close {
    font-size: 85px;
    border: none;
    outline:none;
    text-align: right;
    width: 100%;
  }

  .details-button-container {
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
  }

  .details-button {
    font-size: 25px;
  }

  .details-button:first-of-type {
    margin-right: 15px;
  }

  .button {
    margin-bottom: 20px;
    height: 50px;
    width: 200px;
    background-color: #36E29F;
    font-size: 30px;
    -webkit-transition: background-color .5s;
    transition: background-color .5s;
  }

</style>
