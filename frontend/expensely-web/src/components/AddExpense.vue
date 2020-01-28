<template>
  <div>
      <b-card title="Add Expense" sub-title="Add a new expense to your list">
        <b-card-text>
            <b-form>
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
                    ></b-form-input>
                </b-form-group>

                <b-form-group id="input-group-2" label="Amount" label-for="input-2" description="The amount of money spend.">
                    <b-form-input
                    id="input-2"
                    required
                    placeholder="Enter amount"
                    ></b-form-input>
                </b-form-group>

                <b-button type="submit" variant="primary">Add Expense</b-button>
            </b-form>
        </b-card-text>
    </b-card>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>