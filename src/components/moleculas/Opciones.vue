<template>
    <div id="cosa" :name="name" :index="index">
      <button @click="emitir">
        <div id="contenedor">
            <div id="imag"><img :src="imagen"></div>
            <div id="text"><h2>{{name}}</h2></div>
        </div>
    </button>
    </div>
</template>

<script>
export default {
    props:["name","accion","index","imagen"],
    methods:
    { 
        emitir()
        {
            this.$emit("emitir",this.index);
        }
    }
}
</script>

<style scoped>
    #cosa
    {
        width: 300px;
        height: 90px;
    }
    #contenedor
    {
        float: left;
        width: 100%;
        height: 100%;
    }
    #imag
    {
        float: left;
        width: 30%;
        height: 100%;
    }
    #text
    {
        float: left;
        width: 40%;
        height: 100%;
        padding-top: 5%;
        padding-left: 10%;
    }
    img
    {
        padding-top: 5%;
        width: 80px;
        height: 80px;   
    }
    button
    {
        width: 100%;
        height: 100px;
    }

</style>