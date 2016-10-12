<template>
  <div class="show-notice">
    <div class="notice-list" :style="{transform: 'translateY(-'+noticePosition+'px) translateZ(0px)'}" v-el:roll>
      <p v-for="notice in notices" track-by="$index">{{notice}}</p>
    </div>
  </div>
</template>

<script>
import rAF from '../utils/rAF.js'
export default {
  name: 'RollNotice',
  props: {
    notices: {
      type: Array,
      required: true,
      coerce (data) {
        data.push(data[0])
        return data
      }
    }
  },
  data () {
    return {
      noticePosition: 0
    }
  },
  compiled () {
    let destination = 30
    setInterval(() => {
      if (destination / 30 < this.notices.length) {
        this.move(destination, 500)
        destination += 30
      } else {
        this.noticePosition = 0
        destination = 30
        this.move(destination, 500)
        destination += 30
      }
    }, 2500)
  },
  methods: {
    move (destination, duration) {
      let speed = ((destination - this.noticePosition) * 1000) / (duration * 60)
      let count = 0
      let step = () => {
        this.noticePosition += speed
        count++
        console.log(this.noticePosition)
        rAF(() => {
          if (this.noticePosition < destination) {
            step()
          } else {
            this.noticePosition = destination
          }
        })
      }
      step()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  $notice-height: 30px;
  .show-notice{
    height: $notice-height;
    overflow: hidden;
    vertical-align: middle;
    .notice-list p{
      margin: 0;
      height: $notice-height;
      line-height: $notice-height;
    }
  }
</style>
