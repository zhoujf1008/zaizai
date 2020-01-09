<template>
  <div class="home">
    <!-- 头部图片 -->
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
    
      
      <!-- 内容 -->
      <!-- 分类 6个 -->
      <van-grid :column-num="3">
  <van-grid-item
    v-for="value in categories"
    :key="value.id"
    :icon="value.icon"
    :text="value.name"
  />
</van-grid>
 <!-- 产品 n个 -->

  <briup-product-item
@click="toBuyHandler(p)"
    v-for="p in products"
    :key="p.id"
    :data="p"/>
    
  </div>
</template>
<script>
import {get, post} from '../../http/axios'

export default {
  data(){
return{
categories:[],
products:[]
}
  },
  
  created(){
    //查询栏目信息
    this.loadCategories();
    this.loadProducts();
  },
  methods:{
    toBuyHandler(p){
this.$router.push({
  path:"/manager/order_confirm",
  query:p
})
    },

loadCategories(){
  //加载栏目信息
  let url="/category/findAll"
  get(url).then((response)=>{
    //将查询结果中，显示前六个元素
    this.categories=response.data.slice(0,6);
  })
},
loadProducts(){
  let url="/product/query"
  let param ={
    page:0,pageSize:10,
  }
  post(url,param).then((response)=>{
    this.products=response.data.list;
  })
}

  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>