<template>
  <table class="table">
    <thead>
      <tr>
        <th v-for="(t, index) in titles" :key="index">{{ t }}</th>
      </tr>
    </thead>
    <tbody>
      <!-- 利用临时的来渲染列表 -->
      <tr v-for="item in tempInfo" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.title }}</td>
        <td>{{ item.price_info | priceFormat }}</td>
        <td><button class="btn" @click="remove(item.id)">删除</button></td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td colspan="4">总价为：{{ total | priceFormat }}</td>
      </tr>
    </tfoot>
  </table>
</template>

<script>
  export default {
    name: 'List',
    data() {
      return {
        titles: ['ID', '主标题', '起步价格', '操作'],
        info: [
          {
            id: 287,
            title: '严选新式样板间哈哈',
            price_info: 29.9,
            is_show: true
          },
          {
            id: 286,
            title: '无“油”无虑的甜蜜酥脆哈哈',
            price_info: 45,
            is_show: true
          },
          {
            id: 283,
            title: '孩子成长中少不了的一双鞋',
            price_info: 78,
            is_show: true
          },
          {
            id: 282,
            title: '成就一室笋香1',
            price_info: 121,
            is_show: true
          },
          {
            id: 281,
            title: '条纹新风尚',
            price_info: 29,
            is_show: true
          },
          {
            id: 277,
            title: '治愈生活的满怀柔软',
            price_info: 66.78,

            is_show: true
          },
          {
            id: 274,
            title: '没有软木拖，怎么过夏天',
            price_info: 50.99,
            is_show: true
          },
          {
            id: 272,
            title: '料理也要精细简单',
            price_info: 69,
            is_show: true
          },
          {
            id: 271,
            title: '选式新懒人',
            price_info: 15.3,
            is_show: true
          },
          {
            id: 268,
            title: '米饭好吃的秘诀：会呼吸的锅',
            price_info: 20.1,
            is_show: true
          }
        ],
        tempInfo: []
      };
    },
    // 页面加载完毕 将原始数据给临时数据
    mounted() {
      this.tempInfo = this.info;
      // console.log(this.total);
      // 定义自定义事件
      this.$bus.$on('handleSerchRes', this.handleSerchRes);
    },
    // created() {
    //   this.handleSerch();
    // },
    // 用来做格式化
    filters: {
      priceFormat(val) {
        // console.log(val);
        // return 1;
        return val ? '￥' + val.toFixed(2) + '元' : '兄弟，没有东西噢';
      }
    },
    computed: {
      // 合计总数 使用临时数据
      total() {
        console.log(this.tempInfo.length);
        return this.tempInfo.reduce((pre, cur) => (pre += cur.price_info), 0);
      }
    },
    // 监视 info一变化就修改tempInfo
    watch: {
      info: {
        deep: true,
        handler(newVal) {
          this.tempInfo = newVal;
        }
      }
    },
    methods: {
      // 删除的是真实的info
      remove(iid) {
        // console.log(this.info);
        // console.log(iid);
        if (confirm(`你确定删除吗？`)) {
          this.info = this.info.filter((e) => iid !== e.id);
        }
      },
      // 搜索
      handleSerchRes(txtVal) {
        // console.log(1);
        // console.log(this.txtVal.split(""));
        // 将输入内容转成数组字符  模糊搜索 不用模糊不这么麻烦
        // console.log(txtVal);
        let txtArr = txtVal.split('');
        // console.log(txtArr);
        // 定义一个数组接收
        // let tempArr = [];
        // 遍历真实info符合结果的
        txtArr.map((txt) => {
          // 将搜索结果给临时
          this.tempInfo = this.info.filter((e) => {
            // e.title;
            // console.log(txt);
            // console.log(e.title.indexOf(txt));
            return e.title.indexOf(txt) !== -1;
          });
        });
        // 置空
        txtVal = '';
      }
    }
  };
</script>

<style>
</style>