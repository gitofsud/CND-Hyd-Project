<template>
  <div>
      <Navbar/>
      <b-row>
          <b-col cols="12">
              <div class="mb-3">
                <b-button variant="light" class="mr-3" @click="$router.push('/')">🏡 <strong>Home</strong></b-button>
                <b-button variant="primary" @click="$router.push('analytics')">📈 <strong>Analytics</strong></b-button>
            </div>
          </b-col>
          <!-- <b-col cols="4">
              <b-card bg-variant="light">
                <h2>Total Expense</h2>
                <h1 class="display-3 text-primary">₹{{totalExpense}}</h1>
              </b-card>
          </b-col> -->
          <b-col cols="12" md ="4">
            <Doughnut
                ref="skills_chart"
                v-if="loaded"
                :chart-data="chartdata"
                :options="options">
            </Doughnut>
          </b-col>
          <b-col cols="12" md="8">
              <b-row>
                  <b-col cols="8" md="5">
                        <h4><b-badge variant="success" class="text-success">O</b-badge> Personal</h4>
                        <h4><b-badge variant="warning" class="text-warning">O</b-badge> Travel</h4>
                        <h4><b-badge variant="info" class="text-info">O</b-badge> Entertainment</h4>
                        <h4><b-badge variant="primary" class="text-primary">O</b-badge> Foods</h4>
                        <h4><b-badge variant="danger" class="text-danger">O</b-badge> Bills</h4>
                        <h4 class="my-5"><strong>Total Expense</strong></h4>
                  </b-col>
                  <b-col v-if="loaded" cols="4" md="7">
                      <h4>
                          {{ Math.trunc(((chartdata.datasets[0].data[0])/analytics.total)*100) }}%
                      </h4>
                      <h4>
                          {{ Math.trunc(((chartdata.datasets[0].data[1])/analytics.total)*100) }}%
                      </h4>
                      <h4>
                          {{ Math.trunc(((chartdata.datasets[0].data[2])/analytics.total)*100) }}%
                      </h4>
                      <h4>
                          {{ Math.trunc(((chartdata.datasets[0].data[3])/analytics.total)*100) }}%
                      </h4>
                      <h4>
                          {{ Math.trunc(((chartdata.datasets[0].data[4])/analytics.total)*100) }}%
                      </h4>
                      <h4 class="my-5">
                            ₹ {{ analytics.total }}
                      </h4>
                  </b-col>
              </b-row>
              
          </b-col>
      </b-row>
  </div>
</template>

<script>
import axios from "axios"

import Doughnut from '../components/Doughnut'
import Navbar from '../components/Navbar'

export default {
    components:{
        Navbar,
        Doughnut
    },
    mounted() {
        this.totalExpense = localStorage.getItem('totalExpense');
        this.getAnalytics()
    },
    data() {
        return { 
            loaded:false,
            analytics:'',   
            totalExpense: 0,
            chartdata: {
                labels: ['Personal', 'Travel', 'Entertainment','Foods', 'Bills'],
                datasets: [{
                    label: 'Data One',
                    backgroundColor: ['#28a745', "#ffc107", "#17a2bd", "#007bff", "#dc3545"],
                    data: null
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false
            }
        }
    },
    
    methods: {
        async getAnalytics() {
            console.log("api called")
            var uri = "https://0xq3l9bey8.execute-api.us-east-2.amazonaws.com/dev/analytics"
                const config = {
                method: "get",
                url: uri,
            };
            try {
                const response = await axios(config);
                this.analytics = response.data;
                this.doAnalysis()
            } catch (error) {
                console.log(error);
            }  
        },

        async doAnalysis(){
            this.chartdata.datasets[0].data = [ this.analytics.personal, this.analytics.travel, this.analytics.entertainment, this.analytics.food, this.analytics.bills ]
            this.loaded = true;
        }
    }
}
</script>

<style>

</style>