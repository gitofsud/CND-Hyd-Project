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
      </b-row>
  </div>
</template>

<script>
import Navbar from '../components/Navbar'

export default {
    components:{
        Navbar,
    },
    mounted() {
        this.totalExpense = localStorage.getItem('totalExpense');
    },
    data() {
        return {    
            totalExpense: 0,
            chartdata: {
                labels: ['January', 'February'],
                datasets: [{
                    label: 'Data One',
                    backgroundColor: '#f87979',
                    data: [40, 20]
                }]
        
            },

            options: {
                responsive: true,
                maintainAspectRatio: false
            }
        }
    }   
}
</script>

<style>

</style>