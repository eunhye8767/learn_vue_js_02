<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a  href="javascript:void(0);" @click.prevent="showPopup()" rel="noopener">babel-새창8</a></li>
      <li><a :href=s1 target="_blank" rel="noopener">babel2</a></li>      
      <li><a :href=s1 onclick="window.open(this.href,'comparePopWin','width=1000,height=800,location=no,status=no,scrollbars=no');" rel="noopener">babel-새창</a></li>
      <li><a :href=s1 @click="window.open(s1,'팝업이름','width=1000,height=800,location=no,status=no,scrollbars=no');" rel="noopener">babel-새창2</a></li>
      <li><a href="#" @click.prevent="window.open(s1,'팝업이름','width=1000,height=800,location=no,status=no,scrollbars=no');" rel="noopener">babel-새창5</a></li>
      <li><a :href=s1 target="_blank" v-on:click="window.open(s1,'팝업이름','width=1000,height=800,location=no,status=no,scrollbars=no');" rel="noopener">babel-새창3</a></li>
      <li><button onclick="showMessage()" rel="noopener">babel-새창6</button></li>
      <li><button @click="goUrl" rel="noopener">babel-이동4</button></li>
      <li><button @click="goUrl" disabled="false" rel="noopener">babel-이동5</button></li>
      <li><button @click="goUrl" :disabled="authWorkList1" rel="noopener">babel-disable1</button></li>
      <li><button @click="goUrl" :disabled="authWorkList2" rel="noopener">babel-disable2</button></li>
      <li><button @click="goUrl" disabled="false" rel="noopener">babel-disable3</button></li>
      <li><button @click="goUrl" disabled="disabled" rel="noopener">babel-disable4</button></li>
      <li><button @click="goUrl" disabled rel="noopener">babel-disable5</button></li>
      <li><button @click="goUrl" rel="noopener">babel-disable6</button></li>
      <li><button @click="authWorkList2" rel="noopener">권한체크</button></li>
      <li><button @click="authWorkList2" rel="noopener">{{MyMessage}}</button></li>
      <li><button v-if="yesNoDisable" @click="authWorkList2" rel="noopener">보이게3</button></li>
      <li><button v-show="yesNoDisable" @click="authWorkList2" rel="noopener">보이게4</button></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>
    </ul>
    <h3>Essential Links</h3>
    <ul>
      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>
      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>
    </ul>
    <h3>Ecosystem</h3>
    <ul>
      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>
      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>
      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>
      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      yesNoDisable: true
    }  
  },
  props: {
    msg: String,
    s1: String,
    MyMessage: String
  },
  computed:{
      authWorkList1() {
      console.log("authWorkList1 실행")
      let radio = 'R'
      let report = 'Y'
      let bval = (radio !== 'R' && report !== 'Y')
      console.log((radio !== 'R' && report !== 'Y'))
      console.log(!!(radio !== 'R' && report !== 'Y'))
      console.log(typeof(bval))
      console.log(bval)
      // console.log(!!(radio !== 'R' && report !== 'Y'))      
      return !!(radio !== 'R' && report !== 'Y')
      // return !!bval
      // return !!false
    }
  },
  methods: {
    showPopup() { 
      // alert("pop up")
      window.open(this.s1, "compareWin", "width=1000, height=800, left=800, top=200, location=no,status=no,scrollbars=no")
    },
    goUrl() {
      alert("이동합니다!!")
      location.href ="/"
    },
    authWorkList2() {
      console.log("authWorkList2 실행")
      let radio = 'D'
      let report = 'N'
      let bval = (radio !== 'R' && report !== 'Y')
      console.log((radio !== 'R' && report !== 'Y'))
      console.log(!!(radio !== 'R' && report !== 'Y'))
      console.log(typeof(bval))
      console.log(bval)
      // console.log(!!(radio !== 'R' && report !== 'Y'))      
      return !!(radio !== 'R' && report !== 'Y')
      // return !!bval
      // return !!false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
