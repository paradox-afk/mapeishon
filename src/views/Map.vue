<template>
  <div id="map-view">
     <Mapa id="mapita" :longitud="longitud2 " :latitud="latitud2" :descrip="descrip2" :name="name2" :imagen="imagen2"/>
     <Card styles="top: 10px; left: 5px;">
        <BarraBusqueda @emitir="recibir"/>
     </Card>
     <Card v-if="hack.length!=0" :styles="cuadro">
        <Opciones v-for="(nem,index) in name" :key="nem+index" :index="index" :name="nem" @emitir="seleccion" :imagen="imagen[index]"/>
     </Card>
  </div>
</template>

<script>
import Mapa from "../components/moleculas/Mapa";
import Opciones from "../components/moleculas/Opciones";
import Card from "../components/atomos/Card";
import BarraBusqueda from "../components/moleculas/BarraBusqueda";
export default {
    name:"mapa",
    components: {
        Mapa,
        Card,
        BarraBusqueda,
        Opciones
    },
    data(){
        return{
            longitud:[],
            latitud:[],
            descrip:[],
            name:[],
            imagen:[],
            bandera:false,
            longitud2:"",
            latitud2:"",
            descrip2:"",
            name2:"",
            imagen2:"",
            hack:[],
            cuadro:"top: 50px; left: 5px; height: 365px;",
        };
    },
    methods:
    {
        recibir(response)
        {
            this.hack = response;
            this.longitud = [];
            this.latitud = [];
            this.descrip = [];
            this.name = [];
            this.imagen = [];

            for(var i=0;i<response.data.length;i++)
            {
                this.longitud.push(response.data[i].alt);
                this.latitud.push(response.data[i].lat);
                this.descrip.push(response.data[i].descripcion);
                this.name.push(response.data[i].name);
                this.imagen.push(response.data[i].imagen);
            }

            if(response.data.length >= 4)
            {
                this.cuadro = "top: 50px; left: 5px; height: 365px;";
            }
            else
            {
                switch(response.data.length)
                {
                    case 1:
                        this.cuadro = "top: 50px; left: 5px; height: 110px;";
                        break;
                    case 2:
                        this.cuadro = "top: 50px; left: 5px; height: 200px;";
                        break;
                    case 3:
                        this.cuadro = "top: 50px; left: 5px; height: 290px;";
                        break;
                }
            }
        },
        seleccion(index)
        {
            this.longitud2 = this.hack.data[index].alt;
            this.latitud2 = this.hack.data[index].lat;
            this.descrip2 = this.hack.data[index].descripcion;
            this.name2 = this.hack.data[index].name;
            this.imagen2 = this.hack.data[index].imagen;
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