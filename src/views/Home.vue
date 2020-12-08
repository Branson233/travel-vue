<template>
  <div class="home">
    <home-header></home-header>
    <home-swiper :list="swiperList"></home-swiper>
    <home-icons :list="iconList"></home-icons>
    <home-recommend :list="recommendList"></home-recommend>
    <home-weekend :list="weekendList"></home-weekend>
  </div>
</template>

<script>
import HomeHeader from '../components/Home/Header'
import HomeSwiper from '../components/Home/Swiper'
import HomeIcons from '../components/Home/Icons'
import HomeRecommend from '../components/Home/Recommend'
import HomeWeekend from '../components/Home/Weekend'
import axios from 'axios'
let indexData = require('../../public/mock/index.json')
export default {
  name: 'Home',
  components: {
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend
  },
  data () {
    return {
      swiperList:[],
      iconList:[],
      recommendList:[],
      weekendList:[],
      lastCity:''
    }
  },
  methods: {
    getHomeInfoSucc (res) {
      res=indexData
      if(res.ret && res.data) {
        const data =res.data
        this.swiperList=data.swiperList
        this.iconList=data.iconList
        this.recommendList=data.recommendList
        this.weekendList=data.weekendList
      }
    }
  }, 
  mounted () {
    this.lastCity= this.$store.state.city
    this.getHomeInfoSucc ()
  },
  activated () {
    if (this.lastCity !== this.$store.state.city){
      this.getHomeInfoSucc()
      this.lastCity=this.$store.state.city
    } 
  }
}
</script>
