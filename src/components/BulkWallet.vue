<template>
  <div class="mw9 center ph3-ns bg-white">
    <div class="cf">
      <textarea v-model="text" readonly class="w-90 code pa2 mh2-ns mv2" rows="20"></textarea>
    </div>
  </div>
</template>

<script>
// import QRCode from 'qrcode'
export default {
  props: ['wallets', 'name', 'short', 'working'],
  data () {
    return {
      pubq: '',
      privq: '',
      step: 0
    }
  },
  computed: {
    text: {
      get () {
        if (!this.wallets.length) return 'Click button to generate some addresses'
        if (this.working) return 'Working...'
        let d = new Date()
        let text = `# ${this.name}(${this.short}) bulk wallet. Date: ${d.toLocaleString()}${'\n'}#nn, private key, address${'\n'}`
        this.wallets.forEach((w, i) => {
          text += `${(' ' + (i + 1)).substr(-2)}, ${w.priv}, ${w.pub}${'\n'}`
        })
        return text
      },
      set () {}
    }
  }
}
</script>
