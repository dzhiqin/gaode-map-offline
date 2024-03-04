<script setup>
import { onMounted } from 'vue';
const mapUrl = '.'
console.log('created');
let script = document.createElement('script')
script.src = `${mapUrl}/src/libs/amap/AMap.js`
document.head.appendChild(script)
let map = null
const startLngLat = [118.6218,24.7363]
onMounted(() => {
  console.log('onMounted');
  setTimeout(() => init(),3000)
})
const init = () => {
  const layers = [new AMap.TileLayer({
    getTileUrl: function(x,y,z){
      return `${mapUrl}/MAP_ZXY/${z}/${x}/${y}.png`
    },
    opacity: 1,
    zIndex: 99
  })]
  map = new AMap.Map('container', {
    viewMode: '2D',
    zoom: 12,
    center: startLngLat,
    layers: layers
  })
  AMap.plugin(['AMap.ToolBar'],() => {
    map.addControl(new AMap.ToolBar())
  })
}
</script>

<template>
  
  <div class="map">
    <div id="container"></div>
  </div>
</template>

<style scoped>
#container{
  width: 100vw;
  height: 100vh;
}
/* header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
} */
</style>
