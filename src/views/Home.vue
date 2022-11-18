<template>
    <div>
        <h1>Hello world</h1>
        <Counter :year="2022" :month="10" :date="18" :hours="14" :minute="16" :second="10" :milisecond="10"/>
    </div>
</template>
<script>
import Counter from "../components/Counter.vue"

export default {
    components:{
        Counter
    },
    
}
</script>
<style>
    
</style>