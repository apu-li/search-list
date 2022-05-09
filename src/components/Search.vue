<template>
  <div class="serch">
    名称：
    <input type="text" class="ipt" v-model="txtVal" placeholder="请输入标题" />
    <!-- 不知道为什么不能同时用键盘回车（要鼠标悬浮到按钮）和点击 -->
    <button class="btn" @click="handleSerch">查询</button>
    <!-- <button class="btn" @keyup.enter="handleSerch1">查询</button> -->
  </div>
</template>

<script>
  export default {
    name: 'Search',
    data() {
      return {
        txtVal: ''
      };
    },
    methods: {
      handleSerch() {
        // 非空判断
        if (!this.txtVal.trim()) return alert('请输入内容');
        this.$bus.$emit('handleSerchRes', this.txtVal);
      }
    }
  };
</script>

<style>
</style>