<template>
  <div>
    <el-button size="small" type="success" :disabled="pending" @click="exportCsvBtn">导出 CSV 表格</el-button>
    <div class="control">
      <div>
        <span ref="progress" :style="{ width: `${csvProcess}%` }" class="progress general-5s"></span>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { exportCsv } from '@/utils/xlsx';

export default {
  name: 'BigData',
  data() {
    return {
      pending: false,
      csvProcess: 0,
    };
  },
  methods: {
    // 创建模拟数据
    async exportCsvBtn() {
      try {
        this.pending = true;
        await exportCsv(10000 * 100, 2000, (process) => {
          // 进度条更新
          console.log('process', process);
          this.csvProcess = process;
        });
      } catch (error) {
        // alert(error);
      } finally {
        this.pending = false;
      }
    },
  }

};
</script>

<style>
.title {
  color: #fff;
}
.smooth {
  color: aqua;
}
.control {
  background: rgb(121 121 102 / 30%);
  width: 90%;
  height: 3px;
  border-radius: 5px;
  margin: 10px auto;
}
.control .progress {
  display: block;
  width: 30%;
  height: 3px;
  background: #34c91f;
  border-radius: 5px;
}
.smooth {
  transition: 0.5s linear;
}
.control .timer {
  font-size: 12px;
}
</style>
