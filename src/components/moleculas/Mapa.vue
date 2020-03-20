<template>
  <div :id="id" class="mapota" :longitud="longitud" :latitud="latitud" :descrip="descrip" :name="name" :imagen="imagen">
  </div>
</template>

<script>
var mapboxgl = require('mapbox-gl/dist/mapbox-gl.js');
export default {
    name:"mapa",
    props:["id","longitud","latitud","descrip","name","imagen"],
    data()
    {
        return{
            map:null,
        };
    },
    mounted()
    {
        mapboxgl.accessToken = 'pk.eyJ1IjoibWVtb2xva29raiIsImEiOiJjazdlMmZiaTYwMWRpM2VvYmhrbXY2Z2dtIn0.uJZ46zgJDWrwzRkNCIRlnA';
        this.map = new mapboxgl.Map(
        {
            container: this.id,
            style: 'mapbox://styles/mapbox/streets-v11'
        });
    },
    updated()
    {
        
        mapboxgl.accessToken = 'pk.eyJ1IjoibWVtb2xva29raiIsImEiOiJjazdlMmZiaTYwMWRpM2VvYmhrbXY2Z2dtIn0.uJZ46zgJDWrwzRkNCIRlnA';
        this.map = new mapboxgl.Map(
        {
            container: this.id,
            style: 'mapbox://styles/mapbox/streets-v11'
        });

        
            var popup = new mapboxgl.Popup({ offset: 25}).setHTML("<h2 style='text-align: center;'>"+this.name+"</h2>"+"<p style='text-align: center;'>"+this.descrip+"</p>"+"<img src='"+this.imagen+"' style='width: 220px; height: 100px'>");
            
            var marcador = new mapboxgl.Marker();
            marcador.setLngLat([this.longitud, this.latitud]);
            marcador.addTo(this.map);
            this.map.flyTo(
            {
                center: [this.longitud,this.latitud],
                zoom: 15,
                curve: 1,
                speed: 3,
                easing(t) 
                {
                    return t;
                }
            });

            marcador.setPopup(popup);
        
    }    
}
</script>

<style scoped>
    .mapota{
        height: 100%;
        width: 100%;
    }
</style>