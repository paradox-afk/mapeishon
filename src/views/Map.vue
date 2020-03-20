<template>
  <div id="map-view">
     <Mapa id="mapita" :longitud="longitud " :latitud="latitud" :descrip="descrip" :name="name" :imagen="imagen"/>
     <Card styles="top: 10px; left: 10px;">
    <BarraBusqueda @emitir="recibir"/>
     </Card>
  </div>
</template>

<script>
import Mapa from "../components/moleculas/Mapa";
import Card from "../components/atomos/Card";
import BarraBusqueda from "../components/moleculas/BarraBusqueda";
export default {
    name:"mapa",
    components: {
        Mapa,
        Card,
        BarraBusqueda
    },
    data(){
        return{
            longitud:"",
            latitud:"",
            descrip:"",
            name:"",
            imagen:""
        };
    },
methods:{
    recibir(response)
    {
        this.longitud = response.data[0].alt;
        this.latitud = response.data[0].lat;
        this.descrip = response.data[0].descripcion;
        this.name = response.data[0].name;
        this.imagen = response.data[0].imagen;
    }
}
}
</script>

<style scoped>
    #map-view{
        height: 100vh;
        width: 100vw;
    }
</style>