<template>
  <div class="sphere_container">
      <div class="floor floor_one"></div>
      <div class="floor floor_two"></div>
    <div class="right_anchor">
      <ul>
        <li class="dot" @click="anchors(n)" v-for="(itme,n) in list" :key="n"></li>
      </ul>
    </div>
  </div>
</template>

<script>
import { constants } from 'crypto';
export default {
  data () {
    return {
      steps:0,
      scrolltop : 0 ,//滑轮 距顶部的距离
      list:[1,2],
      floorOne:[]
    }
  },
  mounted(){
    this.getFloorDistance();
    this.getPulleyTopDistance();
  },
  methods:{
    anchors(val){
      for(var net = 0 ; net<= this.floorOne.length-1;net++){
          if(val == net){
            this.pulleyRoll(this.floorOne[net],this.scrolltop);
          }
      }
    },
    /**
     * 滑轮 向上滚动和向下滚动的函数
     * top是楼层距窗体顶部的距离,distance当前滚动条与窗体顶部的距离
     * */
    pulleyRoll(top,distance){
      /*向下滚动*/
      if(distance < top){
        var small_interval = (top-distance)/50;
        var i = 0;
        var timer = setInterval(()=>{
          i++;
          // console.log(distance+= small_interval);
          distance+= small_interval
          document.documentElement.scrollTop = distance;
          if(i == 50){
            clearInterval(timer);
          }
        },10)
      }
      /*向上滚动*/
      else if(distance > top){
        var small_interval = (distance - top)/50;
        var i = 0;
        var timer = setInterval(()=>{
          i ++;
          // console.log(distance -= small_interval);
          distance -= small_interval
          document.documentElement.scrollTop = distance;
          if(i == 50){
            clearInterval(timer);
          }
        },10);
      }
    },
    /**
     * 拿到所有 楼层距窗体顶部的距离
     * */
    getFloorDistance(){
      //拿到每个 楼层距窗体顶部的距离
      for(var i=0;i<this.list.length;i++){
        this.floorOne[i] = document.getElementsByClassName("floor")[i].offsetTop;
        this.floorOne[i] = document.getElementsByClassName('floor')[i].offsetTop;
      }
    },
    /**
     * 滑轮滚动事件 返回滑轮距顶部的距离
     * */
    getPulleyTopDistance(){
      var that = this;
      window.onscroll = function(){
        that.scrolltop = document.documentElement.scrollTop || document.body.scrollTop;
      }
    }
  },
  watch:{
    //监听 滑轮滚动的值的变化 来实现自动锚点
    scrolltop(val){
      val += 200;
    },
    
  }
}
</script>

<style  scoped>

  .floor{
      height: 1000px;
    }
    .floor_one{
      background: #ff7488;
    }
    .floor_two{
      background: #b5ff8a;
    }
    .floor_three{
      background: #6db9ff;
    }
    .floor_four{
      background: #c277ff;
    }
    .floor_five{
      background: #4139ff;
    }
    .no_line{
      width: 2px;
      height: 40px;
      background: none;
      text-align: center;
      border-radius: 0;
      margin: 0 auto;
    }
    .lines{
      width: 2px;
      height: 40px;
      background: #fff;
      text-align: center;
      border-radius: 0;
      margin: 0 auto;
    }
    .right_anchor{
      position: fixed;
      right: 30px;
      top: 30%;
      width: 20px;
      height: 100px;
      z-index: 999;
      
    }
    .dot{
          width: 15px;
          height: 15px;
          border-radius: 100%;
          margin: 0 auto;
          background: #fff;
          margin-bottom: 50px;
        }
    .dot{
          cursor: pointer;
        }

</style>