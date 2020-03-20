<template>
  <div>
      <Entrada v-model="busqueda"/>
      <Boton @click="buscar">Buscar</Boton>
  </div>
</template>

<script>
import Entrada from "../atomos/Entrada";
import Boton from "../atomos/Boton";
import axios from "axios";
import {mapMutations} from "vuex"
export default {
    name:"barraBusqueda",
    components:{
        Entrada,
        Boton
    },
    data(){
        return {
            busqueda:""
        }
    },
    methods:{
        ...mapMutations(["setResultadosMapa"]),
        buscar(){
            if(this.busqueda!=""){
            axios.get("http://localhost:3000/busqueda", {
                params: {
                    search: this.busqueda
                }
            } ).then(response => {
                this.$emit("emitir",response.data);
                this.setResultadosMapa(response.data)
            }).catch(error => console.log(error));
        }
        }
    }
}
</script>
<style>

</style>