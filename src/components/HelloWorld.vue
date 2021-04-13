<template>
  <div v-on:keyup.esc="alert(1)">
    <a-row :style="'text-align: center;font-size: '+fontSize+'px'">
      <a-col :span="24">
        <a-button type="primary" style="margin: 0 10px;" size="small" @click="changeWord">改变文字</a-button>
        <a-button type="primary" style="margin: 0 10px;" size="small" @click="isShowWords=!isShowWords">{{ !isShowWords?"显示":"隐藏" }}上一组文字</a-button>
        <a-button type="primary" style="margin: 0 10px;" size="small" @click="fontSize++">加大文字</a-button>
        <a-button type="primary" style="margin: 0 10px;" size="small" @click="fontSize--">减少文字</a-button>
      </a-col>
      <a-col :span="24">
        <div style=" font-size: 12px;text-align: left;padding: 20px;margin-bottom:10%">
          <span style="display: block;">帮助：盯着中间的字，同时注意两边的文字</span>
          <span style="display: block;">SPACE： 换下一个字符</span>
          <span style="display: block;">CONTROL： 按住显示上一个文字 </span>
          <span style="display: block;">+： 增大文字 </span>
          <span style="display: block;">-： 减小文字 </span>
          <span style="display: block;">文字大小：{{ fontSize }}px</span>
        </div>
      </a-col>
      <a-col :span="4">
        <span v-show="isShowWords">  {{ word1 }}</span>
      </a-col>
      <a-col :span="16">
        <span style="color: red;">看我</span>
      </a-col>
      <a-col :span="4" v-show="isShowWords">
        <span v-show="isShowWords">  {{ word2 }}</span>
      </a-col>

    </a-row>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }, created() {
    document.addEventListener('keydown', this.handleKeyDown)
    document.addEventListener('keyup', this.handleKeyUp)
  },
  data() {
    return {
      isShowWords: true,
      word1: '我',
      word2: '你',
      fontSize: 25,
      KEY_SPACE: 32, //space 键为 32
      KEY_ENTER: 13,  //enter 的键为 13
      KEY_CONTROL: 17, //CONTROL 的键为 17
      KEY_PLUS: 187, //+
      KEY_MINUS: 189 // -
    }
  }, methods: {
    handleKeyDown(e) {
      e.preventDefault() //取消浏览器原有的操作
      var key = window.event.keyCode ? window.event.keyCode : window.event.which
      console.log("=====key down:", key);
      if (key === this.KEY_SPACE) {

        this.changeWord()
      }
      if (key === this.KEY_CONTROL) {
        this.isShowWords = true;
      }
      if (key === this.KEY_PLUS) {
        this.fontSize++;
      }
      if (key === this.KEY_MINUS) {
        this.fontSize--;
      }
    },
    handleKeyUp(e) {

      e.preventDefault(); //取消浏览器原有的操作
      var key = window.event.keyCode ? window.event.keyCode : window.event.which
      console.log("=====key down:key up:", key);
      if (key === this.KEY_CONTROL) {
        this.isShowWords = false;
      }
    },
    getRandomChineseWord() {
      // var _rsl = "";
      // var _randomUniCode = Math.floor(Math.random() * (40870 - 19968) + 19968).toString(16);
      // eval("_rsl=" + '"\\u' + _randomUniCode + '"');
      // return _rsl;
      return Math.ceil(Math.random() * 100)
    },
    changeWord() {
      this.isShowWords = true;
      this.word1 = this.getRandomChineseWord();
      this.word2 = this.getRandomChineseWord();
      setTimeout(() => {
        this.isShowWords = false
      }, 500)
    }
  }
}
</script>
