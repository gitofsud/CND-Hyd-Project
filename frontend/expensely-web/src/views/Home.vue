<template>
  <div class="home">
    <Navbar/>
    <b-row>
      
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
  </div>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import Navbar from '../components/Navbar.vue'
import AddExpense from '../components/AddExpense.vue'
// import Notifications from '../components/Notifications.vue'
import ExpenseCard from '../components/ExpenseCard.vue'

export default {
  name: 'home',
  components: {
    Navbar,
    AddExpense,
    // Notifications,
    ExpenseCard,
  },
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
      Items:'',
      sum: 0,
    }
  },
  methods: {
    async getExpenses() {
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
        console.log(response.data);
      } catch (error) {
        console.log(error);
      }  
    },

    async saveItems() {
      let parsed = await JSON.stringify(this.Items);
      localStorage.setItem('Items', parsed);
    },

    calculateTotalExpense(){
      console.log("called");
      for(var item in this.Items ) {
        this.sum = this.sum + Number(this.Items[item].ExpenseAmt)
        localStorage.setItem('totalExpense', this.sum);
      }
    }
  }
}
</script>
