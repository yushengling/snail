<template>
  <div id="app" @paste="onPaste">
    <router-view></router-view>
  </div>
</template>

<script>
import { clipboard } from 'electron'

export default {
  name: 'snail',
  methods: {
    onPaste (e) {
      const magnetLinks = clipboard.readText().split(/\s+/).filter(str => /^magnet:?[^\\"]+/.test(str))
      this.$electron.ipcRenderer.send('new-torrenting', magnetLinks)
    }
  }
}
</script>

<style lang="scss">
@import '~font-awesome/css/font-awesome.min.css';
@import '~bulma/bulma.sass';
html,
body,
#app {
  height: 100%;
  overflow: hidden;
  transform: translateZ(0);
}
</style>
