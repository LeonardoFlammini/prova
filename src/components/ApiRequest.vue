<script>
import axios from 'axios'
import {store} from "../data/store"
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from 'swiper/vue';

// Import Swiper styles
import 'swiper/css';

import 'swiper/css/navigation';

import 'swiper/css/pagination';
// import required modules
import { Pagination, Navigation } from 'swiper/modules';
export default {
    name: "ApiRequest",
    components:{
        Swiper,
        SwiperSlide,
    },
    data(){
        return {
            store,
            modules: [Pagination, Navigation],
        }
    },
    methods:{
        getApi(){
            const encodedToken = btoa(store.token);
            axios.get(store.apiUrl, {
                headers: {
                    'Authorization': `Basic ${encodedToken}`
                }
            }
            )
            .then(response => {
                store.resultsArray = response.data;
                console.log(store.resultsArray);
            })
            .catch(error => {
                console.error('Errore nella richiesta:', error);
            });
        }
    },
    mounted(){
        this.getApi();
    }
}
</script>

<template>
    <div class="container  m-5">
        <h3 class="p-3">Swiper</h3>

        <div class="swiper-container visible-pc ">
    <swiper
      :slidesPerView="3"
      :navigation="{
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      }"
      :modules="modules"
      class="mySwipe  "
    >
      
      <swiper-slide v-for="apartment in apartments" :key="apartment.id" ><CardSliderHome :apartment="apartment"/>
      </swiper-slide>
      
    </swiper>
    <!-- <div class="swiper-button-next swiper-button"></div>
    <div class="swiper-button-prev swiper-button"></div> -->
  </div>
  <div class="swiper-container visible-smartphone">
    <swiper
      :slidesPerView="1"
      :navigation="{
        nextEl: '.swiper-button-next',
        prevEl: '.swiper-button-prev',
      }"
      :modules="modules"
      class="mySwipe  "
    >
      
      <swiper-slide v-for="component in store.resultsArray" :key="component.id" >
        <div class="card" style="">
            
            <div class="card-body">
                <h5 class="card-title">ID: {{ component.id }}</h5>
                <h5 class="card-title">Category: {{ component.category }}</h5>
                <h5 class="card-title">Currency: {{ component.currency }}</h5>
                <h5 class="card-title">Family: {{ component.family }}</h5>
                <h5 class="card-title">Name: {{ component.name }}</h5>
                <h5 class="card-title">Prezzo: {{ component.prezzo }}</h5>
                <h5 class="card-title">tipologia: {{ component.tipologia }}</h5>
                <ol>
                    <li v-for="(value, key) in component.properties" :key="key">
                        {{ key }}: {{ value }}
                    </li>
                </ol>

                
            </div>
        </div>
      </swiper-slide>
      
    </swiper>
    <div class="swiper-button-next swiper-button"></div>
    <div class="swiper-button-prev swiper-button"></div>
  </div>

    </div>

</template>



<style lang="scss" scoped>

.swiper-container{
  position: relative;
  width: 100%;
  .mySwiper{
    width: 90%;
  }
  .swiper-slide {
    margin-right: 0px !important;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .swiper-button{
    color: #146C94;
  }
}

</style>