<template>
  <div class="new-contact">
    <div class="new-contact__banner">
      <span>Please select a contact from the menu on the left.</span>
      <h3>-OR-</h3>
      <span>Create a new contact:</span>
    </div>
    <div class="new-contact__form">
      <div class="form-block">
        <label class="form-block__label">
          NAME
        </label>
        <input class="form-block__input" v-model="name"/>
      </div>
      <div class="form-block">
        <label class="form-block__label" v-bind:class="{greyed: !name}">
          NUMBER
        </label>
        <input class="form-block__input"  placeholder="optional" v-bind:class="{ineditable: !name}" v-model="number"/>
      </div>
      <div class="form-block">
        <label class="form-block__label" v-bind:class="{greyed: !name}">
          EMAIL
        </label>
        <input class="form-block__input"  placeholder="optional" v-bind:class="{ineditable: !name}" v-model="email"/>
      </div>
      <div class="form-block">
        <label class="form-block__label" v-bind:class="{greyed: !name}">
          NICKNAME
        </label>
        <input class="form-block__input" placeholder="optional"  v-bind:class="{ineditable: !name}" v-model="nickname"/>
      </div>
    </div>
    <button class="button" v-on:click="postNewContact" v-bind:class="{nobutton: !name}">SAVE</button>
  </div>
</template>

<script>
import { mixin as classNamesMixin } from 'vue-classnames';

export default {
    mixins: [classNamesMixin],
    name:'NewContactForm',
    data: function() {
      return {
        name: null,
        number: null,
        email: null,
        nickname: null
      }
    },
    methods: {
      postNewContact: async function() {
        const myHeaders = new Headers()
        myHeaders.append('Content-Type', 'application/json; charset=utf-8')
        myHeaders.append('access-control-allow-origin', '*')
        const nameBody = {
          title: this.name
        }

        if (!this.number && !this.email && !this.nickname) {
          const postFetchNew = await fetch('http://localhost:8000/api/contacts', {
            method: 'POST',
            headers: myHeaders,
            body: JSON.stringify(nameBody)
          })
          const postResult = await postFetchNew.json()
        }
        const postFetchNew = await fetch('http://localhost:8000/api/contacts', {
          method: 'POST',
          headers: myHeaders,
          body: JSON.stringify(nameBody)
        })
        const postResult = await postFetchNew.json()

        const detailsBody = {
          nickname: this.nickname,
          email: this.email,
          number: this.number
        }
        const postFetchDetails = await fetch (`http://localhost:8000/api/contacts/${postResult.id}/details`, {
          method: 'POST',
          headers: myHeaders,
          body: JSON.stringify(detailsBody)
        })
        this.name = null
        this.number = null
        this.email = null
        this.nickname = null
      }
    }
}


</script>

<style>
  .new-contact {
    width: 75vw;
    margin-left: 25vw;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .new-contact__banner {
    padding: 15px;
    text-align: center;
    font-size: 42px;
  }

  .new-contact__form {
    width: 100%;
    text-align: center;

  }

  .form-block {
    text-align: center;
    padding-left: 15%;
    padding-right: 15%;
    font-size: 34px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 22px;
  }

  .form-block__input {
    border: 1px solid #707070;
    padding: 5px;
    font-size: 28px;
  }

  .greyed {
    color: #D9D9D9;
  }

  .ineditable {
    border: 1px solid #D9D9D9;
    pointer-events: none;
  }

  .ineditable::placeholder {
    color: white;
  }

  .button {
    height: 50px;
    width: 200px;
    background-color: #36E29F;
    font-size: 30px;
    -webkit-transition: background-color .5s;
    transition: background-color .5s;
  }
  .nobutton {
    display: none;
  }

  .button:hover {
    background-color: #02AD6B;
  }

  @media (max-width: 930px){
    .form-block {
      text-align: center;
      padding-left: 15%;
      padding-right: 15%;
      font-size: 34px;
      display: flex;
      flex-direction: column;
      margin-bottom: 0px;
    }
  }

  @media (max-width: 1166px) {
    .new-contact__banner {
      font-size: 36px;
    }
  }

</style>
