<template>
  <div id="app">
    <Header msg="One contact list to rule them all..."/>
    <div class="main-container">
      <Sidebar />
      <DetailsView :selectedContactId='selectedContactId' />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Sidebar from './components/Sidebar.vue'
import DetailsView from './components/Details/DetailsView.vue'

export default {
  name: 'app',
  data: function() {
    return {
      selectedContactId: null
    }
  },
  components: {
    Header,
    Sidebar,
    DetailsView
  },
  methods: {
    updateSelectedId: function(event) {
      console.log('event: ', event)
    }
  }
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
