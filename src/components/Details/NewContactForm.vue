<template>
  <div class="new-contact">
    <div class="new-contact__banner">
      <span>Please select a contact from the menu on the left</span>
      <h1>-OR-</h1>
      <span>Create new contact</span>
    </div>
    <div class="new-contact__form">
      <div class="form-block">
        <label class="form-block__label">
          NAME
        </label>
        <input class="form-block__input"/>
      </div>
      <div class="form-block">
        <label class="form-block__label">
          NUMBER
        </label>
        <input class="form-block__input"/>
      </div>
      <div class="form-block">
        <label class="form-block__label">
          EMAIL
        </label>
        <input class="form-block__input"/>
      </div>
      <div class="form-block">
        <label class="form-block__label">
          NICKNAME
        </label>
        <input class="form-block__input"/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name:'NewContactForm',
    data: function() {
      return {

      }
    },
    methods: {
      postNewContact: async function() {

      }
    }
}


</script>

<style>
  .new-contact {
    width: 75vw;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .new-contact__banner {
    text-align: center;
  }

</style>
