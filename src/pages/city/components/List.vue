<template>
  <div class="list" ref="wrapper">
    <div>
      <div class="area">
        <div class="title border-topbottom">当前城市</div>
        <div class="button-list">
          <div class="button-wrapper">
            <div class="button">{{this.$store.state.city}}</div>
          </div>
        </div>
      </div>
      <div class="area">
        <div class="title border-topbottom">热门城市</div>
        <div class="button-list">
          <div @click="handleCityClick(item.name)" class="button-wrapper" v-for="item in hot" :key="item.id">
            <div class="button">{{item.name}}</div>
          </div>
        </div>
      </div>
      <div class="area" v-for="(value, key) in cities" :key="key" :ref="key">
        <div class="title border-topbottom">{{key}}</div>
        <ul class="item-list">
          <li class="item border-bottom" v-for="item in value" :key="item.id" @click="handleCityClick(item.name)">{{item.name}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import Bscroll from 'better-scroll'

export default {
  name: 'CityList',
  props: {
    cities: Object,
    hot: Array,
    letter: String
  },
  mounted () {
    this.scroll = new Bscroll(this.$refs.wrapper, {mouseWheel: true, click: true, tap: true})
  },
  methods: {
    handleCityClick (cityName) {
      this.$store.dispatch('changeCity', cityName)
      this.$router.push('/')
    }
  },
  watch: {
    letter: function () {
      if (this.letter) {
        var element = this.$refs[this.letter][0]
        this.scroll.scrollToElement(element)
      }
    }
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .border-topbottom {
    &:before {
      border-color: #ccc;
    }
    &:after {
      border-color: #ccc;
    }
  }
  .border-bottom {
    &:before {
      border-color: #ccc;
    }
  }
  .list{
    overflow: hidden;
    position: absolute;
    top: 1.58rem;
    left: 0;
    right: 0;
    bottom: 0;
    .title {
      line-height: 0.54rem;
      background-color: #eee;
      padding-left: 0.2rem;
      color: #666;
      font-size: 0.26rem;
    }
    .button-list {
      padding: 0.1rem 0.6rem 0.1rem 0.1rem;
      overflow: hidden;
      .button-wrapper {
        float: left;
        width: 33.33%;
        .button {
          text-align: center;
          margin: 0.1rem;
          padding: 0.1rem 0;
          border: 0.02rem solid #ccc;
          border-radius: 0.06rem;
        }
      }
    }
    .item-list {
      .item {
        line-height: 0.76rem;
        padding-left: 0.2rem;
      }
    }
  }
</style>
