<template>
  <div>
    <v-card>
      <!-- 卡片的头部 -->
      <v-card-title>
        <v-btn color="primary">新增</v-btn>
        <!--空间隔离组件-->
        <v-spacer />
        <!--搜索框，与search属性关联-->
        <v-text-field label="输入关键字搜索" v-model="keyword" append-icon="search" hide-details/>
      </v-card-title>
      <!-- 分割线 -->
      <v-divider/>
      <!--卡片的中部-->
      <v-data-table
        :headers="headers"
        :items="brands"
        :search="search"
        :pagination.sync="pagination"
        :total-items="totalBrands"
        :loading="loading"
        class="elevation-1"
      >
        <template slot="items" slot-scope="props">
          <td>{{ props.item.id }}</td>
          <td class="text-xs-center">{{ props.item.name }}</td>
          <td class="text-xs-center"><img :src="props.item.image" width="130" height="40"></td>
          <td class="text-xs-center">{{ props.item.letter }}</td>
          <td class="justify-center layout">
            <v-btn flat icon color="primary">
              <v-icon>edit</v-icon>
            </v-btn>
            <v-btn flat icon color="error">
              <v-icon>delete</v-icon>
            </v-btn>
          </td>
        </template>
      </v-data-table>
    </v-card>
  </div>
</template>

<script>
    export default {
        name: "MyBrand",
        data () {
          return {
            headers: [ // 头信息
              {text: 'id', align: 'center', value: 'id'},
              {text: '名称', align: 'center', value: 'name', sortable: false},
              {text: 'LOGO', align: 'center', value: 'image', sortable: false},
              {text: '首字母', align: 'center', value: 'letter'},
              {text: '操作', align: 'center', value: 'id', sortable: false}
            ],
            totalBrands: 0, // 总条数
            brands: [], // 当前页品牌数据
            loading: true, // 是否在加载中
            pagination: {}, // 分页信息
            keyword: "", // 搜索条件
          }
        },
        mounted(){ // 渲染后执行
          // 查询数据
          this.loadBrandList();
        },
        watch: {
          // 搜索条件改变时触发查询
          keyword() {
            this.loadBrandList();
          }
        },
        methods:{
          // 从服务的加载数据的方法。
          loadBrandList(){
            // 发起请求
            this.$http.get("/item/brand/list", {
                params: {
                  keyword: this.keyword, // 搜索条件
                }
              }).then(resp => {
                this.brands = resp.items;
              })

            // 模拟延迟一段时间，随后进行赋值
            setTimeout(() => {
              // 然后赋值给brands
              this.brands = brands;
              this.totalBrands = brands.length;
              // 完成赋值后，把加载状态赋值为false
              this.loading = false;
            },400)
          }
        }
    }
</script>

<style scoped>

</style>
