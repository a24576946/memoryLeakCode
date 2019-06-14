<template>
  <div class="hello">
    <h1>{{ msg }}</h1>   
    <div id="map"></div>
  </div>
</template>

<script>
import '../../static/ol/ol-debug'
import '../../static/ol/map2dTools'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      tileLayer:null,
    }
  },
  methods: {

  },
  mounted() {
    let mapTools = new Map2DTools();
    mapTools.map = new ol.Map({
        // rendeder: ["webgl", "canvas"],
        target: "map",
        logo: false,
        loadTilesWhileAnimating: true,
        controls: ol.control
            .defaults({
            attributionOptions: {
                collapsible: true,
                collapsed: true
            }
            })
            .extend([
            new ol.control.Zoom({
                zoomInTipLabel: "放大",
                zoomOutTipLabel: "缩小"
            }),
            new ol.control.ScaleLine(),
            new ol.control.FullScreen({
                tipLabel: "全屏显示",
                label: "\u2922"
            }),
            new ol.control.MousePosition({
                coordinateFormat: ol.coordinate.createStringXY(4),
                projection: "EPSG:4326",
                className: "custom-mouse-position",
                target: document.getElementById("mouse-position")
            })
            ]),
        view: new ol.View({
            projection: "EPSG:3857",
            center: ol.proj.transform([116, 40], "EPSG:4326", "EPSG:3857"),
            minZoom: 2,
            maxZoom: 20,
            zoom: 10
        })
    });
    
    var key = 'pk.eyJ1IjoiYWhvY2V2YXIiLCJhIjoiY2pzbmg0Nmk5MGF5NzQzbzRnbDNoeHJrbiJ9.7_-_gL8ur7ZtEiNwRfCy7Q';
    var source = new ol.source.VectorTile({
        format: new ol.format.MVT({
            featureClass: ol.Feature
        }),
        url: 'https://{a-d}.tiles.mapbox.com/v4/mapbox.mapbox-streets-v6/' + '{z}/{x}/{y}.vector.pbf?access_token=' + key,
        projection: 'EPSG:3857'
    });

    this.tileLayer = new ol.layer.VectorTile({
        declutter: true,
        source: source
    })

    mapTools.map.addLayer(this.tileLayer); 
    
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#map{
    width:600px;
    height:500px;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
