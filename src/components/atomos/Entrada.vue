<template>
  <input ref="input" type="text" @input="input" :value="value">
</template>

<script>
export default {
    name:"Entrada",
    props:[
        "type",
        "value"
    ],
    methods:{
        input(){
            this.$emit("input", this.$refs.input.value)
        }
    }
}
</script>

<style>
    input
    {
        background-color: rgb(179, 228, 115);
        border: solid black;
    }
</style>