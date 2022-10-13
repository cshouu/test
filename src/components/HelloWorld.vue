<template>
  <div class="hello">
    <input type="file" @change="toHtml" ref="input"/>
    <div v-html="html"></div>
  </div>
</template>

<script>
import mammoth from 'mammoth'
export default {
  name: 'HelloWorld',
  data () {
    return {
      value: 'Welcome to Your Vue.js App',
      html: ''
    }
  },
  methods: {
    toHtml () {
      let file = this.$refs.input.files[0]
      let reader = new FileReader()
      reader.onloadend = event => {
        let arrayBuffer = reader.result
        mammoth.convertToHtml({arrayBuffer: arrayBuffer}).then(resultObject => {
          this.html = resultObject.value
          console.log(resultObject.value)
        })
      }
      reader.readAsArrayBuffer(file)
    }
  }
}
</script>
