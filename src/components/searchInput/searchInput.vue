<template>
  <div class='selected-div'>
    <!-- <div class="pos"></div> -->
    <div
      class='table-row'
      v-for='(item, index) in filtedata2'
      :key='item.dictValue'
    >
      <div class='table-item table-item-check'>
        <span>
          <!-- {{ $t('Distance') }} -->
          {{ item.dictLabel }}
        </span>
      </div>
      <el-radio-group
        v-model='item.radio'
        class='table-item-block'
      >
        <div
          class='table-item'
          v-for='(it, indx) in item.list'
        >
          <el-radio
            :label='it.dictValue'
            @change='radioChange(item)'
          >{{ it.dictLabel }}</el-radio>
        </div>

        <div class='table-item'>
          <el-radio
            :label='0'
            @change='radioChange(item)'
          >{{ $t('All') }}</el-radio>
        </div>
      </el-radio-group>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      filtedata2: []
    }
  },
  props: {
    filtedata: {
      type: Array,
      default: []
    }
  },
  methods: {
    radioChange: function (item) {
      console.log(item)
      this.$emit('radioChange', this.filtedata2)
    }
  },
  watch: {
    filtedata: {
      handler: function (val, oldval) {
        this.filtedata2 = JSON.parse(JSON.stringify(this.filtedata))
      },
      deep: true // 对象内部的属性监听，也叫深度监听
    }
  }
}
</script>

<style lang='scss' scoped rel='stylesheet/scss'>
.selected-div {
  background-color: #fff;
  border: 1px solid #dbdbdb;
  // position: relative;
  // .pos {
  //   width: 110px;
  //   height: 12px;
  //   position: absolute;
  //   background-color: #fff;
  //   right: -1px;
  //   top: -11px;
  //   border-left: 1px solid #dbdbdb;
  //   border-right: 1px solid #dbdbdb;
  // }

  .table-row {
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: space-between;

    .table-item {
      padding: 0px 16px;
      height: 60px;
      width: 33.33%;
      border-left: 1px solid #dedede;
      display: flex;
      align-items: center;

      font-size: 14px;
      font-weight: 400;
      color: #333333;

      .tips {
        color: #999999;
      }
    }

    /deep/ .el-input {
      flex: 1;
      background-color: transparent;
      border: none;

      .el-input__inner {
        background-color: transparent;
        border: none;
      }
    }

    /deep/ .el-select {
      flex: 1;
    }

    &:last-child {
      border-top: 1px solid #dedede;
    }
  }

  .table-row {
    border-top: 1px solid #dedede;

    &:first-child {
      border-top: none;
    }
  }

  .el-checkbox {
    display: flex;
    align-items: center;
  }

  .table-item-check {
    width: 241px;
    background: #f3f3f3;
  }

  .table-item-block {
    display: flex;
    width: calc(100% - 214px);

    .table-item {
      flex: 1;
      border-left: none;
    }
  }

  /deep/ .el-radio__input.is-checked .el-radio__inner {
    background-color: #302861;
  }

  /deep/ .el-radio__inner {
    border: 2px solid #302861;
  }
}
</style>
