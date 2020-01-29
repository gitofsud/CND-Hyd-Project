<template>
  <div class="home">
    <Navbar/>
    <b-row>
      <b-col cols="12" md="8">
        <div>
          <img src="../assets/notFound.svg" alt="Not found" width="75%%">
        </div>
      </b-col>
      <b-col cols="12" md="4">
        <AddExpense/>
        <Notifications/>
      </b-col>
    </b-row>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '../components/Navbar.vue'
import AddExpense from '../components/AddExpense.vue'
import Notifications from '../components/Notifications.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    AddExpense,
    Notifications
  }
}
</script>
