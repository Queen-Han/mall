<template>
  <div id="home">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <home-swiper :banners="banners"></home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control :titles="['流行','新款','精选']" class="tab-control"></tab-control>
    <goods-list :goods="goods['pop'].list" />
    
    <ul>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>10</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>10</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>10</li>
      <li>1</li>
      <li>2</li>
      <li>3</li>
      <li>4</li>
      <li>5</li>
      <li>6</li>
      <li>7</li>
      <li>8</li>
      <li>9</li>
      <li>10</li>
    </ul>
  </div>
</template>

<script>

import HomeSwiper from '../home/childComps/HomeSwiper'
import RecommendView from '../home/childComps/RecommendView'
import FeatureView from './childComps/FeatureView'

import NavBar from 'components/common/navbar/NavBar'
import TabControl from 'components/content/tabControl/TabControl'
import GoodsList from 'components/content/goods/GoodsList'

import {getHomeMultidata,getHomeGoods} from 'network/home'


export default {
  name:'Home',
  components:{
    HomeSwiper,
    RecommendView,
    FeatureView,

    NavBar,
    TabControl,
    GoodsList,
  },
  data(){
    return{
      banners:[],
      recommends:[],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]}
      }
    }
  },
  created() {
    //1.请求多个数据
    this.getHomeMultidata()
    //2.请求商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  methods:{
    getHomeMultidata(){
      getHomeMultidata().then(res => {
       console.log(res);
      this.banners = res.data.data.banner.list;
      this.recommends = res.data.data.recommend.list
      })
    },
    getHomeGoods(type){
      const page = this.goods[type].page + 1
      getHomeGoods(type,page).then(res =>{
      console.log(res);
      this.goods[type].list.push(...res.data.data.list)
      this.goods[type].page += 1
      })
    }
  }
}
</script>

<style>
#home{
  padding-top: 44px;
}
  .home-nav{
    /* background-color:pink; */
    background-color: var(--color-tint);/* 使用定义的变量 */
    color: white;

    position: fixed;
    left:0; 
    right: 0;
    top:0;
    z-index: 9;
  }
  .tab-control{
    position: sticky;/* 没有到达指定位置之前默认是sticky，达到指定位置之后是fixed,兼容性不好，但现在是移动端都支持*/
    top: 44px;
  }
</style>