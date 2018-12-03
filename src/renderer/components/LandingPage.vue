<template>
  <div id="editor">
		<!-- <img id="logo" src="~@/assets/logo.png" alt="electron-vue"> -->
    <textarea :value="input" @input="update"></textarea>
    <div v-html="compiledMarkdown"></div>
  </div>
</template>

<script>
import marked from 'marked';

export default {
  data() {
    return {
      input: '',
      audios: {
        do:    new Audio('static/se/do.wav'),
        re:    new Audio('static/se/re.wav'),
        mi:    new Audio('static/se/mi.wav'),
        fa:    new Audio('static/se/fa.wav'),
        so:    new Audio('static/se/so.wav'),
        ra:    new Audio('static/se/ra.wav'),
        ra_hi: new Audio('static/se/ra_hi.wav'),
        si:    new Audio('static/se/si.wav'),
      },
      tetrisMusic: [],
      tetrisMusicIndex: 0,
    };
  },
  created: function() {
    this.tetrisMusic = [
      // ミシドレドシ
      this.audios.mi,
      this.audios.si,
      this.audios.do,
      this.audios.re,
      this.audios.do,
      this.audios.si,
      // ララドミレド
      this.audios.ra,
      this.audios.ra,
      this.audios.do,
      this.audios.mi,
      this.audios.re,
      this.audios.do,
      // シシドレミドララ
      this.audios.si,
      this.audios.si,
      this.audios.do,
      this.audios.re,
      this.audios.mi,
      this.audios.do,
      this.audios.ra,
      this.audios.ra,
      // レファラソファ
      this.audios.re,
      this.audios.fa,
      this.audios.ra_hi,
      this.audios.so,
      this.audios.fa,
      // ミミドミレド
      this.audios.mi,
      this.audios.mi,
      this.audios.do,
      this.audios.mi,
      this.audios.re,
      this.audios.do,
      // シシドレミドララ
      this.audios.si,
      this.audios.si,
      this.audios.do,
      this.audios.re,
      this.audios.mi,
      this.audios.do,
      this.audios.ra,
      this.audios.ra,
    ];

    console.log(this.tetrisMusic);
  },
  computed: {
    compiledMarkdown() {
      return marked(this.input, { sanitize: true });
    },
  },
  methods: {
    update(e) {
      this.tetrisMusic[this.tetrisMusicIndex].play();
      this.tetrisMusicIndex += 1
      if (this.tetrisMusicIndex >= this.tetrisMusic.length) { this.tetrisMusicIndex = 0 }
      this.input = e.target.value;
    },
  },
};
</script>

<style>
html, body, #editor {
  margin: 0;
  font-family: 'Helvetica Neue', Arial, sans-serif;
  color: #333;
}

textarea, #editor div {
  display: inline-block;
  width: 49%;
  height: 100vh;
  vertical-align: top;
  box-sizing: border-box;
  padding: 0 20px;
}

textarea {
  border: none;
  border-right: 1px solid #ccc;
  resize: none;
  outline: none;
  background-color: #f6f6f6;
  font-size: 14px;
  font-family: 'Monaco', courier, monospace;
  padding: 20px;
}

code {
  color: #f66;
}
</style>
