<template>
    <div id="city" :class="'city'+$store.state.service.lang">
        <c-title :hide="false" :text='language.title'></c-title>
        <div class="input">
            <i class="iconfont icon-sousuo1"></i>
            <input type="text" :placeholder="language.placeTip" v-model="sokey" />
        </div>

        <!--<mt-navbar v-model="selected" id='selecteds' fixed>
              <mt-tab-item id="1">{{language.domestic}}</mt-tab-item>
              <mt-tab-item id="2">{{language.international}}</mt-tab-item>
            </mt-navbar>-->
        <!-- tab-container -->
        <div>
        <!-- <mt-tab-container v-model="selected"> -->
            <div v-show="selected==1">
            <!-- <mt-tab-container-item id="1"> -->
                <!-- right fixed -->
                <ul class="innerRig">
                    <li class="quickLocation">{{language.positioned}}</li>
                    <li class="letter" @click="goSoso('A')">A</li>
                    <li class="letter" @click="goSoso('B')">B</li>
                    <li class="letter" @click="goSoso('C')">C</li>
                    <li class="letter" @click="goSoso('D')">D</li>
                    <li class="letter" @click="goSoso('E')">E</li>
                    <li class="letter" @click="goSoso('F')">F</li>
                    <li class="letter" @click="goSoso('G')">G</li>
                    <li class="letter" @click="goSoso('H')">H</li>
                    <li class="letter" @click="goSoso('J')">J</li>
                    <li class="letter" @click="goSoso('K')">K</li>
                    <li class="letter" @click="goSoso('L')">L</li>
                    <li class="letter" @click="goSoso('M')">M</li>
                    <li class="letter" @click="goSoso('N')">N</li>
                    <li class="letter" @click="goSoso('P')">P</li>
                    <li class="letter" @click="goSoso('Q')">Q</li>
                    <li class="letter" @click="goSoso('R')">R</li>
                    <li class="letter" @click="goSoso('S')">S</li>
                    <li class="letter" @click="goSoso('T')">T</li>
                    <li class="letter" @click="goSoso('W')">W</li>
                    <li class="letter" @click="goSoso('X')">X</li>
                    <li class="letter" @click="goSoso('Y')">Y</li>
                    <li class="letter" @click="goSoso('Z')">Z</li>
                </ul>
                <!-- left inner -->
                <div class="content">
                    <div class="list" v-for="(item,i) in searchData" :key='i'>
                        <p class="title">{{item.sign}}</p>
                        <ul>
                            <li :key='i' v-for="(city,i) in item.citys" @click="chooseCity($event)">{{city}}</li>
                        </ul>
                    </div>
                </div>
            <!-- </mt-tab-container-item> -->
            </div>
            <div v-show="selected==1">
            <!-- <mt-tab-container-item id="2"> -->
                <ul class="innerRig">
                    <li class="quickLocation">{{language.positioned}}</li>
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
                        <p class="title">{{language.currentAddr}}</p>
                        <div id="map">
                            <i class="iconfont icon-sousuo1"></i> 加载中</div>
                    </div>
                    <div class="list" :key='i' v-for="(item,i) in allCitys">
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

import trainCity_controller from './trainCity_controller';
export default trainCity_controller;		
</script>
<style lang="scss" rel="stylesheet/scss" scoped>
.citych {
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
      // background: url(../../../../assets/images/search.png) no-repeat 0.5rem 0.625rem #fff;
    }
  }

  .mint-navbar.is-fixed {
    top: 2.5rem;
    margin-top: 3.4375rem;
  }

  .mint-navbar .mint-tab-item.is-selected {
    border-bottom: 0.125rem solid #3a3d3d;
    color: #677573;
  }

  .mint-navbar .mint-tab-item:first-child {
    border-right: #e3e3e3 solid 0.0625rem;
  }

  .innerRig {
    position: fixed;
    width: 2.5rem;
    z-index: 99;
    right: 0;
    top: 5.625rem;
    bottom: 0;
    padding-top: 0.3125rem;
    padding-bottom: 0.3125rem;
    margin-top: 0;
    margin-bottom: 0;
    display: flex;
    flex-direction: column;
    color: #8c8c8c;
    background: none;
    font-size: 12px;

    li {
      line-height: 1.5rem;
    }
  }

  .content {
    margin-top: 3.125rem;
    text-align: left;

    .location {
      padding: 0 0.875rem;

      .title {
        color: #666;
        font-size: 12px;
        line-height: 1.875rem;
      }

      div {
        width: 30%;
        height: 1.875rem;
        background: #fff;
        font-size: 16px;
        color: #333;
        line-height: 1.875rem;
        text-align: center;
        border-radius: 0.25rem;
      }
    }

    .list {
      .title {
        background: #fafafa;
        color: #333;
        font-size: 14px;
        line-height: 1.5rem;
        height: 1.5rem;
        padding-left: 0.875rem;
      }

      ul {
        padding-left: 1rem;
        background: #fff;

        li {
          width: 100%;
          height: 2.25rem;
          line-height: 2.25rem;
          border-bottom: 0.0625rem solid #ebebeb;
          color: #333;
          font-size: 14px;
        }

        li:last-child {
          border: 0;
        }
      }
    }
  }
}

.citywei {
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
    top: 141px;
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
    text-align: right;

    .location {
      padding: 0 0.9375rem;
      height: 3.75rem;

      .title {
        color: #666;
        font-size: 12px;
        line-height: 1.875rem;
      }

      div {
        width: 30%;
        height: 1.875rem;
        background: #fff;
        font-size: 16px;
        color: #333;
        line-height: 1.875rem;
        text-align: center;
        border-radius: 0.25rem;
        float: right;
      }
    }

    .list {
      .title {
        color: #666;
        font-size: 12px;
        line-height: 1.25rem;
        padding-right: 0.9375rem;
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
        }

        li:last-child {
          border: 0;
        }
      }
    }
  }
}
</style>