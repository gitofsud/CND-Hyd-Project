<template>
  <div> 
      <b-card sub-title="Add a new expense to your list" header="featured" header-bg-variant="primary" header-text-variant="white" border-variant="primary" class="rounded">
          <template v-slot:header>
      <h4 class="mb-0">Add Expense</h4>
    </template>
        <b-card-text>
            <b-form @submit.prevent="onSubmit">
                <h6>    
                    <b-form-group
                        id="input-group-1"
                        label="Title"
                        label-for="input-1"
                        description="A small title that will best describw your expense"
                    >
                        <b-form-input
                        id="input-1"
                        type="text"
                        required
                        placeholder="Enter title"
                        v-model="item.title"
                        ></b-form-input>
                    </b-form-group>
                </h6>

                <h6>
                    <b-form-group id="input-group-2" label="Amount" label-for="input-2" description="The amount of money spend.">
                        <b-form-input
                        id="input-2"
                        type="number"
                        required
                        placeholder="Enter amount"
                        v-model="item.amt"
                        ></b-form-input>
                    </b-form-group>
                </h6>
                
                <h6>
                    <b-form-group id="input-group-3" label="Category" label-for="input-3" description="A category to categorise your expense">
                        <b-form-select v-model="item.category" :options="options"></b-form-select>
                    </b-form-group>
                </h6>

                <b-button type="submit" variant="primary" v-if="!loading">
                    Add Expense
                </b-button>

                <b-button disabled variant="primary" v-if="loading">
                    <b-spinner small label="Spinning"></b-spinner>
                     Adding Expense
                </b-button>
            </b-form>
        </b-card-text>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            loading:false,
            item:{
                amt:'',
                category:null,
                title:'',
            },
            selected: null,
            options: [
            { value: null, text: 'Please select a category' },
            { value: 'Bills', text: 'Bills' },
            { value: 'Entertainment', text: 'Entertainment' },
            { value: 'Food', text: 'Food' },
            { value: 'Travel', text: 'Travel' },
            { value: 'Personal', text: 'Personal' }
            ]
        }
    },

    methods: {
        async onSubmit() {
            this.loading=true
            console.log("called")
            const config = {
                method: "post",
                url: "https://0xq3l9bey8.execute-api.us-east-2.amazonaws.com/dev/expense",
                data: this.item
            };
            try {
                await axios(config);
                this.loading = false;
            } catch (error) {
                console.log(error)
            }
            this.item.title = "";
            this.item.amt = "";
            this.item.category = null;
        }
    }
}
</script>

<style>

</style>