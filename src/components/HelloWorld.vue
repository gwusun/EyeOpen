<template>
  <div class="hello">
    <a-row :style="'text-align: center;font-size: '+fontSize+'px'">
      <a-col :span="24">
        <div style="height: 200px;font-size: 12px;">
          使用方式：点击改变更换文字；盯着中间的字，同时注意两边的文字
        </div>
      </a-col>
      <a-col :span="4">
        <span v-show="isShow">  {{ word1 }}</span>
      </a-col>
      <a-col :span="16">
        <span style="color: red;">看我</span>
      </a-col>
      <a-col :span="4" v-show="isShow">
        <span v-show="isShow">  {{ word2 }}</span>
      </a-col>
      <a-col :span="24">
        <div style="height: 200px;font-size: 12px;"></div>
        <a-button @click="changeWord">改变</a-button>
        <a-button @click="isShow=true">显示</a-button>
        <a-button @click="fontSize++">加大文字</a-button>
        <a-button @click="fontSize--">减少文字</a-button>
      </a-col>
    </a-row>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      isShow: true,
      word1: '我',
      word2: '你',
      fontSize: 18
    }
  }, methods: {
    getRandomChineseWord() {
      var _rsl = "";
      var _randomUniCode = Math.floor(Math.random() * (40870 - 19968) + 19968).toString(16);
      eval("_rsl=" + '"\\u' + _randomUniCode + '"');
      return _rsl;
    },
    changeWord() {
      this.isShow = true;
      this.word1 = this.getRandomChineseWord();
      this.word2 = this.getRandomChineseWord();
      setTimeout(() => {
        this.isShow = false
      }, 500)
    }
  }
}
</script>
