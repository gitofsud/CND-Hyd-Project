<template>
    <div>
        <div @click="$router.push('/')" class="logo">Expense<span style="color: #007BFF; font-weight: bold">ly.</span></div>
        
        <hr>
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.logo {
    font-size: 2em;    
}
.logo:hover{
    cursor: pointer;
}
</style>