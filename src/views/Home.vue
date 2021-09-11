<template>
  <div class="home">
    <top-view />
    <sales-view />
    <buttom-view />
    <map-view />
  </div>
</template>

<script>
import TopView from '@/components/TopView'
import SalesView from '@/components/SalesView'
import ButtomView from '@/components/ButtomView'
import MapView from '@/components/MapView'

export default {
  name: 'Home',
  components: {
    TopView,
    SalesView,
    ButtomView,
    MapView
  }
}
</script>

<style lang="scss">
  .home {
    border: 3px solid #cc0;
    width: 100%;
    height: 100%;
    padding: 20px;
    background-color: #eee;
    box-sizing: border-box;
  }
</style>
