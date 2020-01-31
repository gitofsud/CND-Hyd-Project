<template>
  <div>
      <Navbar/>
      <b-row>
          <b-col cols="2">
                <img src="../assets/car.svg" alt="" width="100%" v-if="item.ExpenseCategory == 'Travel'">
                <img src="../assets/clapper.svg" alt="" width="90%" v-if="item.ExpenseCategory == 'Entertainment'">
                <img src="../assets/food.svg" alt="" width="100%" v-if="item.ExpenseCategory == 'Food'">
                <img src="../assets/bill.svg" alt="" width="100%" v-if="item.ExpenseCategory == 'Bills'">
                <img src="../assets/parachute.svg" alt="" width="100%" v-if="item.ExpenseCategory == 'Personal'">     
          </b-col>
          <b-col class="display-4" cols="10">
                <b-badge variant="warning" class="p-2" v-if="item.ExpenseCategory == 'Travel'">{{item.ExpenseCategory}}</b-badge>
                <b-badge variant="info" class="p-2" v-if="item.ExpenseCategory == 'Entertainment'">{{item.ExpenseCategory}}</b-badge>
                <b-badge variant="primary" class="p-2" v-if="item.ExpenseCategory == 'Food'">{{item.ExpenseCategory}}</b-badge>
                <b-badge variant="danger" class="p-2" v-if="item.ExpenseCategory == 'Bills'">{{item.ExpenseCategory}}</b-badge>
                <b-badge variant="success" class="p-2" v-if="item.ExpenseCategory == 'Personal'">{{item.ExpenseCategory}}</b-badge>
                <div>
                    {{item.ExpenseTitle}}
                </div>
                    
          </b-col>
      </b-row>
      <b-row>
          <b-col cols="12" class="display-1">
              ₹{{item.ExpenseAmt}}
          </b-col>
      </b-row>
      <b-row>
          <b-col cols=12>
            <b-button variant="danger" @click="deleteItem($route.params.id)">
              <strong>Delete</strong>
              <b-spinner small label="Spinning" v-if="loading"></b-spinner>
            </b-button>
          </b-col>
      </b-row>
  </div>
</template>

<script>
import axios from "axios"

import Navbar from '../components/Navbar.vue'
export default {
    components:{
        Navbar,
    },

    created() {
        this.getExpenseById(this.$route.params.id)
    },

    mounted() {
        if(localStorage.getItem(this.$route.params.id)){
            try {
                this.item = JSON.parse(localStorage.getItem(this.$route.params.id));
            } catch(e) {
                this.getExpenseById()
            }
        } else {
            this.getExpenseById()
        }
    },

    data() {
        return {
            loading: false,
            item: '',
        }
    },

    methods: {
        async getExpenseById(id) {
            console.log("api called")
            var uri = "https://0xq3l9bey8.execute-api.us-east-2.amazonaws.com/dev/expense/"+id
                const config = {
                method: "get",
                url: uri,
            };
            try {
                const response = await axios(config);
                this.item = response.data;
                this.saveItem(id)
            } catch (error) {
                console.log(error);
            }  
        },

        async saveItem(id) {
            let parsed = await JSON.stringify(this.item);
            localStorage.setItem(id, parsed);
        },

        async deleteItem(id) {
            this.loading = true;
            console.log("delete  called")
            var uri = "https://0xq3l9bey8.execute-api.us-east-2.amazonaws.com/dev/expense/"+id
                const config = {
                method: "delete",
                url: uri,
            };
            try {
                await axios(config);
                console.log("deleted")
                this.loading = false
                localStorage.removeItem(id);
                this.$router.push('/');
            } catch (error) {
                console.log(error);
            }  
        },
    }

}
</script>

<style>

</style>