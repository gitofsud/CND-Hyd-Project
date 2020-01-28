<template>
  <div class="home">
    <Navbar/>
    <b-row>
      <b-col cols="8">Expenses</b-col>
      <b-col cols="12" md="4">
        <AddExpense/>

      </b-col>
    </b-row>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from '../components/Navbar.vue'
import AddExpense from '../components/AddExpense.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    AddExpense
  }
}
</script>
