<template>
  <div id="trafficCity" :class="'trafficCity'+$store.state.service.lang">
    <c-title :hide="false" :text='language.title'></c-title>
    <div class="input">
      <i class="iconfont icon-sousuo1"></i>
      <input type="text" :placeholder="language.placeTip"/>
    </div>

    <van-tabs v-model="selected" id='selecteds'>
      <van-tab name="1" :title="language.domestic"></van-tab>
      <van-tab name="2" :title="language.International"></van-tab>
    </van-tabs>
    <div style="height: 2.5rem;"></div>
    <!-- tab-container -->
    <div>
      <!-- <mt-tab-container v-model="selected"> -->
      <div v-show="selected==1">
        <!-- <mt-tab-container-item id="1"> -->
        <!-- right fixed -->
        <ul class="innerRig">
          <li class="quickLocation">{{language.positiona}}</li>
          <li class="letter" data-id="1">A</li>
          <li class="letter" data-id="2">B</li>
          <li class="letter" data-id="3">C</li>
          <li class="letter" data-id="4">D</li>
          <li class="letter" data-id="5">E</li>
          <li class="letter" data-id="6">F</li>
          <li class="letter" data-id="7">G</li>
          <li class="letter" data-id="8">H</li>
          <li class="letter" data-id="9">J</li>
          <li class="letter" data-id="10">K</li>
          <li class="letter" data-id="11">L</li>
          <li class="letter" data-id="12">M</li>
          <li class="letter" data-id="13">N</li>
          <li class="letter" data-id="14">P</li>
          <li class="letter" data-id="15">Q</li>
          <li class="letter" data-id="16">R</li>
          <li class="letter" data-id="17">S</li>
          <li class="letter" data-id="18">T</li>
          <li class="letter" data-id="19">W</li>
          <li class="letter" data-id="20">X</li>
          <li class="letter" data-id="21">Y</li>
          <li class="letter" data-id="22">Z</li>
        </ul>
        <!-- left inner -->
        <div class="content">
          <div class="location">
            <p class="title">{{language.currentLocation}}</p>
            <div class="current">
              <span id="map"> </i>{{language.loading}}</span>
            </div>

          </div>
          <div class="list" v-for="(item,i) in allCitys" :key='i'>
            <p class="title">{{item.sign}}</p>
            <ul>
              <li :key='i' v-for="(city,i) in item.citys" @click="chooseCity($event)">{{city}}</li>
            </ul>
          </div>
        </div>
        <!-- </mt-tab-container-item> -->
      </div>
      <div v-show="selected==2">
        <!-- <mt-tab-container-item id="2"> -->
        <ul class="innerRig">
          <li class="quickLocation">{{language.positiona}}</li>
          <li class="letter" data-id="1">A</li>
          <li class="letter" data-id="2">B</li>
          <li class="letter" data-id="3">C</li>
          <li class="letter" data-id="4">D</li>
          <li class="letter" data-id="5">E</li>
          <li class="letter" data-id="6">F</li>
          <li class="letter" data-id="7">G</li>
          <li class="letter" data-id="8">H</li>
          <li class="letter" data-id="9">J</li>
          <li class="letter" data-id="10">K</li>
          <li class="letter" data-id="11">L</li>
          <li class="letter" data-id="12">M</li>
          <li class="letter" data-id="13">N</li>
          <li class="letter" data-id="14">P</li>
          <li class="letter" data-id="15">Q</li>
          <li class="letter" data-id="16">R</li>
          <li class="letter" data-id="17">S</li>
          <li class="letter" data-id="18">T</li>
          <li class="letter" data-id="19">W</li>
          <li class="letter" data-id="20">X</li>
          <li class="letter" data-id="21">Y</li>
          <li class="letter" data-id="22">Z</li>
        </ul>
        <!-- left inner -->
        <div class="content">
          <div class="location">
            <p class="title">{{language.currentLocation}}</p>
            <div class="current">
              <span id="map2"></i> {{language.loading}}</span>
            </div>

          </div>
          <div :key='i' class="list" v-for="(item,i) in allCitys">
            <p class="title">{{item.sign}}</p>
            <ul>
              <li :key='i' v-for="(city,i) in item.citys" @click="chooseCity($event)">{{city}}</li>
            </ul>
          </div>
        </div>
        <!-- </mt-tab-container-item> -->
      </div>
      <!-- </mt-tab-container> -->
    </div>
    <!-- tab-containerEnd -->
  </div>
</template>
<script>
import cTitle from "components/title";
// import { mapState,mapMutations } from 'vuex';

require("c-swipe/dist/swipe.css");
export default {

  data() {
    return {
      language: {},

      selected: "1",
      allCitys: [
        { sign: "A", citys: ["鞍山", "安阳", "安顺", "安庆"] },
        { sign: "B", citys: ["北京", "蚌埠", "包头", "保定", "白银", "宝山"] },
        { sign: "C", citys: ["重庆", "成都", "长沙", "承德"] },
        { sign: "D", citys: ["大连", "大庆", "大同", "丹东", "大冶"] },
        { sign: "E", citys: ["鞍山", "安阳", "安顺", "安庆"] }
      ]
    };
  },

  components: { cTitle },
  methods: {
    onLoaddd() {
      var geolocation = new BMap.Geolocation();
      geolocation.getCurrentPosition(function(r) {
        if (this.getStatus() == BMAP_STATUS_SUCCESS) {

          console.log("您的位置：" + r.point.lng + "," + r.point.lat);
          var geoc = new BMap.Geocoder();
          var pt = new BMap.Point(r.point.lng, r.point.lat);

          geoc.getLocation(pt, function(rs) {
            var addComp = rs.addressComponents;
            document.getElementById("map").innerHTML = "<i class='iconfont icon-sousuo1'></i>" + addComp.city;
            document.getElementById("map2").innerHTML = "<i class='iconfont icon-sousuo1'></i>" + addComp.city;
            //							alert(addComp.province + ", " + addComp.city + ", " + addComp.district + ", " + addComp.street + ", " + addComp.streetNumber);
          });

        } else {
          alert("failed" + this.getStatus());
        }
      }, {
        enableHighAccuracy: true
      });
    },

    chooseCity(e) {
      var texta = e.currentTarget.innerHTML;
      this.$router.push(this.fun.getUrl("trafficIndex", { cityName: texta }));
    },
    //初始化语言
    initLang() {
      if (sessionStorage.languageService) {
        this.language = JSON.parse(sessionStorage.languageService).trafficCity;
      } else {
        this.language = this.$store.state.service.languageService.trafficCity;
      }
    }
  },
  //实时监测this.$store.state.service.chinese的变化，获取最新的语言包
  computed: {
    getLangState() {
      return this.$store.state.service.languageService;
    }
  },
  watch: {
    getLangState(val) {
      if (val) {
        this.language = JSON.parse(sessionStorage.languageService).trafficCity;
      } else {
        this.language = this.$store.state.service.languageService.trafficCity;
      }
    }
  },

  mounted() {
    this.onLoaddd();
    this.initLang();
  },

  activated() {
    this.$store.commit("onload");
  }

};
</script>
<style lang="scss" rel="stylesheet/scss" scoped>
  .trafficCitych {
    .input {
      padding: 0.625rem 5%;
      position: fixed;
      z-index: 999;
      background: #fff;
      width: 100%;
      border-bottom: solid 0.0625rem #ebebeb;

      i {
        position: absolute;
        left: 2.75rem;
        line-height: 1.875rem;
      }

      input {
        background-color: #fafafa;
        width: 90%;
        height: 1.875rem;
        border-radius: 0.3125rem;
        padding-left: 1.875rem;
        border: 0;
        outline: 0;
        // background:url(../../../../assets/images/search.png) no-repeat 0.625rem 0.625rem #fff;
      }
    }

    .van-tabs {
      top: 36px;
      margin-top: 3.4375rem;
      position: fixed;
      left: 0;
      right: 0;
    }

    .mint-navbar .mint-tab-item.is-selected {
      height: 2.5rem;
      line-height: 2.5rem;
      border-bottom: 0.125rem solid #1bba9e;
      color: #1bba9e;
    }

    .mint-tab-item {
      padding: 0.75rem 0;
    }

    .innerRig {
      position: fixed;
      width: 2.5rem;
      z-index: 99;
      right: 0;
      top: 8.5rem;
      bottom: 0;
      display: flex;
      flex-direction: column;
      color: #8c8c8c;

      li {
        flex: 1;
      }
    }

    .content {
      margin-top: 6rem;
      text-align: left;

      .location {
        padding: 0 0.875rem;
        margin-bottom: 0.625rem;

        .title {
          color: #666;
          font-size: 14px;
          line-height: 2.25rem;
        }

        .current {
          display: flex;
          flex-wrap: wrap;
          padding: 0 1.25rem;
        }

        span {
          float: left;
          padding: 0 1rem;
          margin-right: 0.375rem;
          margin-bottom: 0.375rem;
          background: #fff;
          border: solid 0.0625rem #ebebeb;
          font-size: 12px;
          color: #333;
          height: 1.875rem;
          line-height: 1.875rem;
          text-align: center;
          border-radius: 0.25rem;
        }
      }

      .list {
        .title {
          color: #666;
          font-size: 12px;
          line-height: 1.5rem;
          padding-left: 0.875rem;
          background-color: #fafafa;
        }

        ul {
          padding-left: 2.875rem;
          background: #fff;

          li {
            width: 100%;
            height: 2.25rem;
            line-height: 2.25rem;
            border-bottom: 0.0625rem solid #ebebeb;
            color: #333;
          }

          li:last-child {
            border: 0;
          }
        }
      }
    }
  }

  .trafficCitywei {
    .input {
      margin-top: 2.5rem;
      padding: 0.625rem 5%;
      position: fixed;
      z-index: 999;
      background: #eee;
      width: 90%;

      input {
        width: 90%;
        height: 2.1875rem;
        border-radius: 0.375rem;
        padding-left: 1.875rem;
        border: 0;
        outline: 0;
        background: url(../../../../assets/images/search.png) no-repeat 0.625rem 0.625rem #fff;
      }
    }

    .mint-navbar.is-fixed {
      top: 2.5rem;
      margin-top: 3.4375rem;
    }

    .mint-navbar .mint-tab-item.is-selected {
      border-bottom: 0.125rem solid #1bba9e;
      color: #1bba9e;
    }

    .mint-navbar .mint-tab-item:first-child {
      border-right: #e3e3e3 solid 0.0625rem;
    }

    .innerRig {
      position: fixed;
      width: 2.5rem;
      z-index: 99;
      left: 0;
      top: 8.8125rem;
      bottom: 0;
      display: flex;
      flex-direction: column;
      color: #1bba9e;
      background: #fff;

      li {
        flex: 1;
      }
    }

    .content {
      margin-top: 6.25rem;
      padding-top: 0.625rem;
      text-align: left;

      .location {
        padding: 0 0.9375rem;
        height: 4.0625rem;

        .title {
          color: #666;
          font-size: 12px;
          line-height: 1.875rem;
          text-align: right;
        }

        .current {
          display: flex;
          flex-wrap: wrap;
          padding: 0 1.25rem;
        }

        span {
          float: left;
          padding: 0 1rem;
          margin-right: 0.375rem;
          margin-bottom: 0.375rem;
          background: #fff;
          border: solid 0.0625rem #ebebeb;
          font-size: 12px;
          color: #333;
          height: 1.875rem;
          line-height: 1.875rem;
          text-align: center;
          border-radius: 0.25rem;
        }
        // div{
        //     width:30%;
        //     height:1.875rem;
        //     background:#fff;
        //     font-size:16px;
        //     color:#333;
        //     line-height:1.875rem;
        //     text-align:center;
        //     border-radius:0.25rem;
        //     float: right;
        // }
      }

      .list {
        .title {
          color: #666;
          font-size: 12px;
          line-height: 1.25rem;
          padding-right: 0.9375rem;
          text-align: right;
        }

        ul {
          padding-right: 2.875rem;
          background: #fff;

          li {
            width: 100%;
            height: 1.875rem;
            line-height: 1.875rem;
            border-bottom: 0.0625rem solid #ccc;
            color: #333;
            text-align: right;
          }

          li:last-child {
            border: 0;
          }
        }
      }
    }
  }
</style>