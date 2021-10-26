<template>
    <div>
      <div class="lottery-container">
        <div class="lottery-part">
          <ul ref="list1">
            <li class="lottery-item" v-for="(item,index) in giftList" :key="index">
              {{ item }}
            </li>
          </ul>
        </div>

        <div class="lottery-part">
          <ul ref="list2">
            <li class="lottery-item" v-for="(item,index) in giftList" :key="index">
              {{ item }}
            </li>
          </ul>
        </div>

        <div class="lottery-part">
          <ul ref="list3">
            <li class="lottery-item" v-for="(item,index) in giftList" :key="index">
              {{ item }}
            </li>
          </ul>
        </div>
      </div>

      <button type="button" class="start-button" @click="startAction">开始</button>
    </div>
</template>

<script>
export default {
  data () {
    return {
      giftList: [1, 2, 3, 4, 5, 6, 7, 8],
      playFlag: true,
      skew1: 55, // 偏移1
      skew2: 55, // 偏移2
      skew3: 55 // 偏移3
    }
  },
  computed: {
  },
  created () {
    this.giftList = this.giftList.concat(this.giftList)
  },
  mounted () {
    this.$refs.list1.style.top = -(this.$refs.list1.offsetHeight / 2) + this.skew1 + 'px'
    this.$refs.list2.style.top = -(this.$refs.list2.offsetHeight / 2) + this.skew2 + 'px'
    this.$refs.list3.style.top = -(this.$refs.list3.offsetHeight / 2) + this.skew3 + 'px'
  },
  methods: {
    startAction () {
      if (!this.playFlag) {
        return false
      }

      this.playFlag = false

      const speed = 5

      const num1 = Math.floor(Math.random() * 7) + 1 // 结束点 num+1最终结束点  对接接口中礼物的index
      const num2 = Math.floor(Math.random() * 7) + 1 // 结束点 num+1最终结束点  对接接口中礼物的index
      const num3 = Math.floor(Math.random() * 7) + 1 // 结束点 num+1最终结束点  对接接口中礼物的index

      const circle = Math.floor(Math.random() * 3) + 1 // 最低圈数3

      let count1 = 0 // 圈数
      let count2 = 0 // 圈数
      let count3 = 0 // 圈数

      // list1
      const itemOffHeight1 = this.$refs.list1.offsetHeight / 16 * num1 // 结束item
      const _timer1 = setInterval(() => {
        const _top = this.$refs.list1.offsetTop
        this.$refs.list1.style.top = _top + speed + 'px'

        if (Math.abs(this.$refs.list1.offsetTop) <= itemOffHeight1 && count1 > circle) {
          this.$refs.list1.style.top = _top + this.skew1 + 'px'

          clearInterval(_timer1)
        }

        // 循环
        if (Math.abs(this.$refs.list1.offsetTop) <= 0) {
          this.$refs.list1.style.top = -(this.$refs.list1.offsetHeight / 2) + 'px'
          count1 += 1
        }
      }, 1)

      setTimeout(() => {
        // list2
        const itemOffHeight2 = this.$refs.list2.offsetHeight / 16 * num2 // 结束item
        const _timer2 = setInterval(() => {
          const _top = this.$refs.list2.offsetTop
          this.$refs.list2.style.top = _top + speed + 'px'

          if (Math.abs(this.$refs.list2.offsetTop) <= itemOffHeight2 && (count2 > circle + 1)) {
            this.$refs.list2.style.top = _top + this.skew2 + 'px'

            clearInterval(_timer2)
          }

          // 循环
          if (Math.abs(this.$refs.list2.offsetTop) <= 0) {
            this.$refs.list2.style.top = -(this.$refs.list2.offsetHeight / 2) + 'px'
            count2 += 1
          }
        }, 1)
      }, 10)

      setTimeout(() => {
        // list3
        const itemOffHeight3 = this.$refs.list3.offsetHeight / 16 * num3 // 结束item
        const _timer3 = setInterval(() => {
          const _top = this.$refs.list3.offsetTop
          this.$refs.list3.style.top = _top + speed + 'px'
          //  && count3 > count2
          if (Math.abs(this.$refs.list3.offsetTop) <= itemOffHeight3 && (count3 > circle + 2)) {
            this.$refs.list3.style.top = _top + this.skew3 + 'px'

            clearInterval(_timer3)
            this.playFlag = true
          }

          // 循环
          if (Math.abs(this.$refs.list3.offsetTop) <= 0) {
            this.$refs.list3.style.top = -(this.$refs.list3.offsetHeight / 2) + 'px'
            count3 += 1
          }
        }, 1)
      }, 20)
    }
  }
}
</script>

<style lang="scss" scoped>
  *{
    padding: 0;
    margin: 0;
  }

  ul,li{
    list-style: none;
  }

  .lottery-container{
    width: 390px;
    height: 220px;
    margin: 0 auto;
    background-color: bisque;
    display: flex;
    justify-content: space-around;

    .lottery-part{
      position: relative;
      width: 110px;
      height: 220px;
      overflow-y: hidden;

      ul{
        position: absolute;
        top: 0;

        .lottery-item{
          height: 110px;
          line-height: 110px;
          width: 110px;
          text-align: center;
          background: rebeccapurple;
        }
      }
    }
  }
</style>
