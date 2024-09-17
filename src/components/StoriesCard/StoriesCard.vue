<template>
  <ion-card v-for="is in isElVisible" :key="is.id">
    <ion-card-header>
      <ion-card-title>{{ is.city }}</ion-card-title>
      <ion-button v-if="!is.status" @click="doText(true, is.id)">Подробнее</ion-button>
      <ion-button v-else="is.status" @click="doText(false, is.id)">Скрыть</ion-button>
    </ion-card-header>

    <ion-card-content v-if="is.status">
      {{ is.description }}
      <ion-card-content v-for="(imgs, index) in is.img" :key="is.id">
        <img :src="imgs">
        <h3>{{ is.title[index] }}</h3>
      </ion-card-content>
    </ion-card-content>
  </ion-card>

  <!-- <ion-card>
    <ion-card-header>
      <ion-card-title>Березовик</ion-card-title>
      <ion-button v-if="!isElVisible" @click="doText(true)">Show</ion-button>
      <ion-button v-else="isElVisible" @click="doText(false)">Hide</ion-button>
    </ion-card-header>

    <ion-card-content v-if="isElVisible">
    </ion-card-content>
  </ion-card> -->


  <ion-card>
    <ion-card-header>
      <ion-card-title>City Do-Do list</ion-card-title>
    </ion-card-header>
    <ion-card-header v-for="item in cityTask" :key="item.id">
      <ion-card-title v-if="!item.status">{{ item.title }}</ion-card-title>
      <ion-card-title v-else style="text-decoration: line-through solid !important;">{{ item.title }}</ion-card-title>
      <ion-button v-if="!item.status" @click="setDoneCity(item.id)">✔️</ion-button>
      <ion-button v-else @click="removeCity(item.id)">❌</ion-button>
    </ion-card-header>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
  IonButton
} from '@ionic/vue'

import { ref } from 'vue'

const isElVisible = ref([
  {
    id: 0,
    status: false,
    city: 'Тейково',
    description: 'Тейково - начало маршрута',
  },
  {
    id: 1,
    status: false,
    city: 'Березовик',
    description: 'Березовик',
    img: [
      '/src/components/img/img1-city1.jpg',
      '/src/components/img/img2-city1.jpg',
      '/src/components/img/img3-city1.jpg',
      '/src/components/img/img4-city1.jpg'

    ],
    title: [
      'Источник иконы Божией Матери «Всех Скорбящих Радость»',
      'Источник святого Архистратига Михаила',
      'Могила Парвицкого',
      'Церковь иконы Божией Матери «Всех скорбящих Радость»'
    ]
  },
  {
    id: 2,
    status: false,
    city: 'Богатырёво',
    description: 'Богатырёво',
    img: [
      '/src/components/img/img1-city2.jpg',
      '/src/components/img/img2-city2.jpg',
    ],
    title: [
      'Мемориал Великой Отечественной войны',
      'Церковь Троицы Живоначальной',
    ]
  },
  {
    id: 3,
    status: false,
    city: 'Златоуст',
    description: 'Златоуст',
    img: [
      '/src/components/img/img1-city3.jpg',
      '/src/components/img/img2-city3.jpg',
      '/src/components/img/img3-city3.jpg',
      '/src/components/img/img4-city3.jpg',
    ],
    title: [
      'Купель ',
      'Покровское подворье Введенского женского монастыря',
      'Церковь в Златоусте',
      'Церковь Воскресения Христова'
    ]
  },
  {
    id: 4,
    status: false,
    city: 'Клементьево',
    description: 'Клементьево',
    img: [
      '/src/components/img/img1-city4.jpg',
    ],
    title: [
      'Церковь Спаса Всемилостивого',
    ]
  },
  {
    id: 5,
    status: false,
    city: 'Озеро Красный остров',
    description: 'Озеро Красный остров',
    img: [
      '/src/components/img/img1-city5.jpg',
      '/src/components/img/img2-city5.jpg',
    ],
    title: [
      'Общий вид',
      'Остров',
    ]
  },
  {
    id: 6,
    status: false,
    city: 'Озеро Рубское',
    description: 'Озеро Рубское',
    img: [
      '/src/components/img/img1-city6.jpg',
    ],
    title: [
      'Общий вид',
    ]
  },
  {
    id: 7,
    status: false,
    city: 'Озеро Рубское',
    description: 'Озеро Рубское',
    img: [
      '/src/components/img/img1-city7.jpg',
    ],
    title: [
      'Общий вид',
    ]
  },
  {
    id: 8,
    status: false,
    city: 'Пелгусово',
    description: 'Пелгусово',
    img: [
      '/src/components/img/img1-city8.jpg',
    ],
    title: [
      'Стела',
    ]
  },
  {
    id: 9,
    status: false,
    city: 'Сахтыш',
    description: 'Сахтыш',
    img: [
      '/src/components/img/img1-city9.jpg',
      '/src/components/img/img2-city9.jpg',
    ],
    title: [
      'Церковь Михаила Архангела',
      'Церковь Николая Чудотворца',
    ]
  },
  {
    id: 10,
    status: false,
    city: 'Хомутово',
    description: 'Хомутово',
    img: [
      '/src/components/img/img1-city10.jpg',
      '/src/components/img/img2-city10.jpg',
      '/src/components/img/img3-city10.jpg',
    ],
    title: [
      'Казанская церковь',
      'Церковная лавка',
      'Церковь Преображения',
    ]
  },
  {
    id: 11,
    status: false,
    city: 'Чернцы',
    description: 'Чернцы',
    img: [
      '/src/components/img/img1-city11.jpg',
      '/src/components/img/img2-city11.jpg',
    ],
    title: [
      'Центр культуры',
      'Церковь Живоначальной Троицы',
    ]
  },
  {
    id: 12,
    status: false,
    city: 'Шилыково',
    description: 'Шилыково - финал маршрута',
    img: [
      '/src/components/img/img1-city12.jpg',
    ],
    title: [
      'Сергиева пустынь',
    ]
  },
])

const doText = (e, id) => {
  isElVisible.value == isElVisible.value.map(x => {
    if (x.id === id)
      x.status = e
    return x
  })
}

const cityTask = ref([
  { id: 0, title: 'Тейково - точка A', status: false },
  { id: 1, title: 'Березовик - точка 1', status: false },
  { id: 2, title: 'Богатырево  - точка 2', status: false },
  { id: 3, title: 'Златоуст - точка 3', status: false },
  { id: 4, title: 'Клементьево - точка 4', status: false },
  { id: 5, title: 'Озеро Красный остров  - точка 5', status: false },
  { id: 6, title: 'Озеро Черное - точка 6', status: false },
  { id: 7, title: 'Озеро Рубское - точка 7', status: false },
  { id: 8, title: 'Пелгусово - точка 8', status: false },
  { id: 9, title: 'Сахтыш - точка 9', status: false },
  { id: 10, title: 'Хомутово - точка 10', status: false },
  { id: 11, title: 'Чернцы - точка 11', status: false },
  { id: 12, title: 'Шилыково - точка B', status: false },
])

const setDoneCity = (id) => {
  cityTask.value == cityTask.value.map(x => {
    if (x.id === id)
      x.status = true
    return x
  })
}

const removeCity = (id) => {
  cityTask.value = cityTask.value.filter(y => y.id !== id)
}

</script>

<style>
ul {
  list-style-type: none;
  /* Убирает буллиты */
}

img {
  max-width: 40%;
  height: auto;
  width: auto\9;
  /* ie8 */
}
</style>

<style src="./StoriesCard.scss"></style>
