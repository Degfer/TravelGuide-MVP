<style>
#container {
  width: 500px;
  height: 300px;
}
</style>


<template>
  <ion-content>
    <ion-card-content>
      <div id="container"></div>
    </ion-card-content>
    <stories-card />
  </ion-content>
</template>

<script setup lang="ts">
import { IonContent, IonCardContent } from '@ionic/vue'

import { StoriesCard } from '../StoriesCard'
// Импортируйте плагин как ES-модуль...
import { Directions } from '@2gis/mapgl-directions';


import { load } from '@2gis/mapgl';
// or const { load } = require('@2gis/mapgl');

load().then((mapglAPI) => {
  const map = new mapglAPI.Map('container', {
    center: [40.53814510956976, 56.85739083355663],
    zoom: 13,
    key: 'e91cb49e-23e7-4762-8f34-74f62409afbb',
  });


  const directions = new Directions(map, {
    directionsApiKey: 'e91cb49e-23e7-4762-8f34-74f62409afbb',
  });

  directions.carRoute({
    points: [
      [40.53814510956976, 56.85739083355663],
      [40.64318407257083, 56.81709743134971],
      [40.33557008214316, 56.847305246655125],
      [40.799181281969474, 56.89327783947368],
      [40.74950141007863, 56.815095452231546],
      [40.69338976287097, 56.84473867369666],
      [40.71164694528135, 56.84750341928817],
      [40.61455105382886, 56.73207292985499],
      [40.71562091715357, 56.941429936038716],
      [40.41871873799819, 56.7966772284858],
      [40.666570659772134, 56.80345003878791],
      [40.762225542082035, 56.86345255757626],
      [40.73705850042061, 56.922360962855]
    ],
  });

});


</script>

<style src="./HomePage.scss"></style>
