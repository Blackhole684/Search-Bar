<template>
  <div class="input-select">
    <p
      v-if="!inputData2[0].arr.length && !inputData2[1].arr.length"
      class="empty"
    >
      No data
    </p>
    <div v-for="item in inputData2" v-else :key="item.name" class="list">
      <h3 v-if="item.arr.length > 0">{{ item.name }}:</h3>
      <p v-for="it in item.arr" :key="it.id" @click="slectedP(it)">
        {{ it.name }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputData2: []
    }
  },
  props: {
    inputData: {
      type: Array,
      default: []
    }
  },
  methods: {
    radioChange: function(item) {
      this.$emit('radioChange', this.inputData)
    },
    slectedP: function(item) {
      this.$emit('togVisible', item)
    }
  },
  watch: {
    inputData: {
      handler: function(val, oldval) {
        this.inputData2 = JSON.parse(JSON.stringify(this.inputData))
      },
      deep: true // 对象内部的属性监听，也叫深度监听
    }
  }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.input-select {
  background-color: #fff;
  max-height: 300px;
  overflow-y: auto;

  .empty {
    font-size: 14px;
    color: #606266;
    line-height: 34px;
    cursor: pointer;
    padding: 0 20px;
  }

  .list {
    h3 {
      font-size: 12px;
      color: #000;
      line-height: 30px;
      padding: 0 20px;
      font-weight: 800;
      margin-bottom: 0;
    }

    p {
      font-size: 14px;
      color: #606266;
      line-height: 34px;
      cursor: pointer;
      padding: 0 20px;

      &:hover {
        background-color: #f5f7fa;
      }
    }
  }
}
</style>
