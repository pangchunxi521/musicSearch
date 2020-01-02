<template>
  <div class="one">
    <input type="text" v-model="searchname"><button @click="search">搜索</button>
    <ul>
      <li v-for="(item,i) in shuzu" :key="i">
        <img :src=" item.pic">
        <a :href="item.url" target="_blank">{{item.title}}--{{item.author}}</a>
      </li>
    </ul>
    <ul>
      <li v-for=" (item,i) in waitBuy" :key="i">
        <p>{{i}} -- {{item}}</p>
      </li>
    </ul>
    <button @click="playSong">按钮</button>
    <br>
    <br>
    <br>
    <br>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: '1212121',
      shuzu: [],
      searchname: ''
    }
  },
  mounted: function () {
    setTimeout(() => {

    }, 1000)
  },
  beforeCreate: function () {
    console.log(this.waitBuy)
  },
  methods: {
    skyapi: function (name) {
      var that = this
      this.axios.get('/api/searchMusic?name=' + name).then(function (response) {
        console.log(response.data.code)
        for (let i = 0; i < (response.data.result).length; i++) {
          that.shuzu.push((response.data.result)[i])
          console.log(response.data.result[i])
        }
      }).catch(function (error) {
        console.log(error)
      })
    },
    search: function () {
      this.shuzu = []
      this.skyapi(this.searchname)
    },
    time: function () {
      console.log(this.searchname)
    },
    playSong: function () {
      this.axios.get('/aapi/#/song?id=3409461').then(function (response) {
        console.log(response)
      }).catch(function (error) {
        console.log(error)
      })
    }
  }
}
</script>
<style>
  a {
    text-decoration: none;
    text-align: center;
    display: inline-block
  }

  li {
    text-align: left;
    list-style-type: none;
  }

  img {
    width: 100px;
    height: 100px;
  }
</style>
