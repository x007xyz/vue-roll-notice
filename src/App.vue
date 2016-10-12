<template>
  <div id="app">
    <h1>信息滚动</h1>
    <roll-notice :notices="['msg1', 'msg2', 'msg3']"></roll-notice>
  </div>
</template>

<script>
export default {
  components: {
    RollNotice: require('./components/RollNotice')
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  font-family: Source Sans Pro, Helvetica, sans-serif;
}
</style>
