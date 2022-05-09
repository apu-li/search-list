<template>
  <div id="app">
    <div class="contain">
      <Search></Search>
      <List></List>
    </div>
  </div>
</template>

<script>
  import List from './components/List.vue';
  import Search from './components/Search.vue';
  export default {
    name: 'App',
    components: {
      List,
      Search
    }
  };
</script>

<style>
  div,
  p,
  input {
    padding: 0;
    margin: 0;
    color: #333;
    font-size: 14px;
  }
  .contain {
    margin: 20px;
  }
  .ipt {
    outline: none;
    border: 1px solid #999;
    width: 130px;
    height: 30px;
    border-radius: 6px;
    padding-left: 10px;
    margin-right: 10px;
  }
  .btn {
    color: #fff;
    width: 50px;
    height: 30px;
    background-color: #87ceeb;
    border: none;
    border-radius: 10px;
  }
  .table,
  th,
  td {
    border: 1px solid #999;
  }
  .table {
    margin-top: 10px;
    border-collapse: collapse;
  }
  th,
  td {
    text-align: left;
    padding: 10px 6px;
    width: 136px;
  }
</style>
