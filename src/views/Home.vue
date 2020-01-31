<template>
  <div class="home">
    <Navbar/>
    <b-row>
      <b-col>
        <div class="mb-3">
            <b-button variant="primary" @click="$router.push('/')">🏡 <strong>Home</strong></b-button>
            <b-button variant="light" class="mx-3" @click="$router.push('analytics')">📈 <strong>Analytics</strong></b-button>
            <b-button variant="light" @click="getExpenses()">
              <i class="fas fa-sync-alt" v-if="!loading"></i>
              <b-spinner small label="Spinning" v-if="loading"></b-spinner>
            </b-button>
        </div>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="12" md="8">
        <div>
          <b-row>
            <b-col cols="12" md="4" v-for="item in Items" :key="item.ExpenseId">
              <ExpenseCard
                :id="item.ExpenseId"
                :title="item.ExpenseTitle"
                :amount="item.ExpenseAmt"
                :category="item.ExpenseCategory"
              />
            </b-col>
          </b-row>
        </div>
      </b-col>
      <b-col cols="12" md="4">
        <b-alert show variant="primary"  dismissible fade>
        <h3>Total Expense</h3>
        <h1>₹{{sum}}</h1>

        </b-alert>
        <AddExpense/>
        <!-- <Notifications/> -->
      </b-col>
    </b-row>
    <Footer/>
  </div>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import Navbar from '../components/Navbar.vue'
import AddExpense from '../components/AddExpense.vue'
// import Notifications from '../components/Notifications.vue'
import ExpenseCard from '../components/ExpenseCard.vue'
import Footer from '../components/Footer.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    AddExpense,
    // Notifications,
    ExpenseCard,
    Footer
  },
  // computed() {
  //   this.sum = localStorage.getItem('totalExpense')
  // },

  mounted(){
    if(localStorage.getItem('Items')){
      try {
        this.Items = JSON.parse(localStorage.getItem('Items'));
      } catch(e) {
        this.getExpenses()
      }
    } else {
      this.getExpenses()
    }
    if(localStorage.getItem('totalExpense')){
      this.sum = localStorage.getItem('totalExpense')
    } else {
      this.calculateTotalExpense()
    }
    // this.calculateTotalExpense()
  },
  data() {
    return {
      loading: false,
      Items:'',
      sum: 0,
    }
  },
  methods: {
    async getExpenses() {
      this.loading = true
      console.log("api called")
      var uri = "https://0xq3l9bey8.execute-api.us-east-2.amazonaws.com/dev/expense"
        const config = {
        method: "get",
        url: uri,
        // headers: {
        //   "Access-Control-Allow-Origin": "*"
        // },
      };
      try {
        const response = await axios(config);
        this.Items = response.data;
        this.saveItems()
        this.calculateTotalExpense()
        this.loading = false;
      } catch (error) {
        console.log(error);
      }  
    },

    async saveItems() {
      let parsed = await JSON.stringify(this.Items);
      localStorage.setItem('Items', parsed);
    },

    calculateTotalExpense(){
      localStorage.setItem('totalExpense', 0);
      this.sum = 0;
      for(var item in this.Items ) {
        this.sum = this.sum + Number(this.Items[item].ExpenseAmt)
        localStorage.setItem('totalExpense', this.sum);
      }
    }
  }
}
</script>
