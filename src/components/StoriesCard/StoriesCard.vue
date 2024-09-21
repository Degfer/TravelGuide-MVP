<template>
  <ion-card v-for="is in isElVisible" :key="is.id">
    <ion-card-header>
      <ion-card-title>{{ is.city }}</ion-card-title>
      <ion-button v-if="!is.status" @click="doText(true, is.id)"
        >Подробнее</ion-button
      >
      <ion-button v-else="is.status" @click="doText(false, is.id)"
        >Скрыть</ion-button
      >
    </ion-card-header>

    <ion-card-content v-if="is.status">
      {{ is.description }}
      <ion-card-content v-for="(imgs, index) in is.img" :key="is.id">
        <img :src="imgs" />
        <h3 v-if="is.title">{{ is.title[index] }}</h3>
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
      <ion-card-title
        v-else
        style="text-decoration: line-through solid !important"
        >{{ item.title }}</ion-card-title
      >
      <ion-button v-if="!item.status" @click="setDoneCity(item.id)"
        >✔️</ion-button
      >
      <ion-button v-else @click="removeCity(item.id)">❌</ion-button>
    </ion-card-header>
  </ion-card>
</template>

<script setup lang="ts">
import {
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardTitle,
  IonButton,
} from '@ionic/vue'

import { ref } from 'vue'

import Image1City1 from '../img/img1-city1.jpg'
import Image2City1 from '../img/img2-city1.jpg'
import Image3City1 from '../img/img3-city1.jpg'
import Image4City1 from '../img/img4-city1.jpg'

import Image1City2 from '../img/img1-city2.jpg'
import Image2City2 from '../img/img2-city2.jpg'

import Image1City3 from '../img/img1-city3.jpg'
import Image2City3 from '../img/img2-city3.jpg'
import Image3City3 from '../img/img3-city3.jpg'
import Image4City3 from '../img/img4-city3.jpg'

import Image1City4 from '../img/img1-city4.jpg'

import Image1City5 from '../img/img1-city5.jpg'
import Image2City5 from '../img/img2-city5.jpg'

import Image1City6 from '../img/img1-city6.jpg'

import Image1City7 from '../img/img1-city7.jpg'

import Image1City8 from '../img/img1-city8.jpg'

import Image1City9 from '../img/img1-city9.jpg'
import Image2City9 from '../img/img2-city9.jpg'

import Image1City10 from '../img/img1-city10.jpg'
import Image2City10 from '../img/img2-city10.jpg'
import Image3City10 from '../img/img3-city10.jpg'

import Image1City11 from '../img/img1-city11.jpg'
import Image2City11 from '../img/img2-city11.jpg'

import Image1City12 from '../img/img1-city12.jpg'

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
    img: [Image1City1, Image2City1, Image3City1, Image4City1],
    title: [
      'Источник иконы Божией Матери «Всех Скорбящих Радость»',
      'Источник святого Архистратига Михаила',
      'Могила Парвицкого',
      'Церковь иконы Божией Матери «Всех скорбящих Радость»',
    ],
  },
  {
    id: 2,
    status: false,
    city: 'Богатырёво',
    description: 'Богатырёво',
    img: [Image1City2, Image2City2],
    title: [
      'Мемориал Великой Отечественной войны',
      'Церковь Троицы Живоначальной',
    ],
  },
  {
    id: 3,
    status: false,
    city: 'Златоуст',
    description: 'Златоуст',
    img: [Image1City3, Image2City3, Image3City3, Image4City3],
    title: [
      'Купель ',
      'Покровское подворье Введенского женского монастыря',
      'Церковь в Златоусте',
      'Церковь Воскресения Христова',
    ],
  },
  {
    id: 4,
    status: false,
    city: 'Клементьево',
    description: 'Клементьево',
    img: [Image1City4],
    title: ['Церковь Спаса Всемилостивого'],
  },
  {
    id: 5,
    status: false,
    city: 'Озеро Красный остров',
    description: 'Озеро Красный остров',
    img: [Image1City5, Image2City5],
    title: ['Общий вид', 'Остров'],
  },
  {
    id: 6,
    status: false,
    city: 'Озеро Рубское',
    description: 'Озеро Рубское',
    img: [Image1City6],
    title: ['Общий вид'],
  },
  {
    id: 7,
    status: false,
    city: 'Озеро Рубское',
    description: 'Озеро Рубское',
    img: [Image1City7],
    title: ['Общий вид'],
  },
  {
    id: 8,
    status: false,
    city: 'Пелгусово',
    description: 'Пелгусово',
    img: [Image1City8],
    title: ['Стела'],
  },
  {
    id: 9,
    status: false,
    city: 'Сахтыш',
    description: 'Сахтыш',
    img: [Image1City9, Image2City9],
    title: ['Церковь Михаила Архангела', 'Церковь Николая Чудотворца'],
  },
  {
    id: 10,
    status: false,
    city: 'Хомутово',
    description: 'Хомутово',
    img: [Image1City10, Image2City10, Image3City10],
    title: ['Казанская церковь', 'Церковная лавка', 'Церковь Преображения'],
  },
  {
    id: 11,
    status: false,
    city: 'Чернцы',
    description: 'Чернцы',
    img: [Image1City11, Image2City11],
    title: ['Центр культуры', 'Церковь Живоначальной Троицы'],
  },
  {
    id: 12,
    status: false,
    city: 'Шилыково',
    description: 'Шилыково - финал маршрута',
    img: [Image1City12],
    title: ['Сергиева пустынь'],
  },
])

const doText = (e: boolean, id: number) => {
  isElVisible.value ==
    isElVisible.value.map((x) => {
      if (x.id === id) x.status = e
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

const setDoneCity = (id: number) => {
  cityTask.value ==
    cityTask.value.map((x) => {
      if (x.id === id) x.status = true
      return x
    })
}

const removeCity = (id: number) => {
  cityTask.value = cityTask.value.filter((y) => y.id !== id)
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
