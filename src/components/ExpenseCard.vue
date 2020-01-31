<template>
  <div>
      <b-card class="mb-4 rounded hoverable" @click="$router.push({name: 'details', params: { id: id}})">
          <b-row>
              <b-col>
                <div id="amount">
                    <h1 class="text-primary">
                        ₹{{amount}}
                    </h1>
                    
                </div>
              </b-col>
              <b-col>
                  <center>
                    <img src="../assets/car.svg" alt="" width="100%" v-if="category == 'Travel'">
                    <img src="../assets/clapper.svg" alt="" width="90%" v-if="category == 'Entertainment'">
                    <img src="../assets/food.svg" alt="" width="100%" v-if="category == 'Food'">
                    <img src="../assets/bill.svg" alt="" width="100%" v-if="category == 'Bills'">
                    <img src="../assets/parachute.svg" alt="" width="100%" v-if="category == 'Personal'">
                  </center>
              </b-col>
          </b-row>
            <h5>{{title}}</h5>
            <b-badge variant="warning" class="p-2" v-if="category == 'Travel'">{{category}}</b-badge>
            <b-badge variant="info" class="p-2" v-if="category == 'Entertainment'">{{category}}</b-badge>
            <b-badge variant="primary" class="p-2" v-if="category == 'Food'">{{category}}</b-badge>
            <b-badge variant="danger" class="p-2" v-if="category == 'Bills'">{{category}}</b-badge>
            <b-badge variant="success" class="p-2" v-if="category == 'Personal'">{{category}}</b-badge>
      </b-card>
  </div>
</template>

<script>

export default {
  props: [
    "id",
    "title",
    "amount",
    "category",
  ],
  
}
</script>

<style>

.hoverable:hover {
  cursor: pointer;
  background-color: #EDF2F7;
}
</style>