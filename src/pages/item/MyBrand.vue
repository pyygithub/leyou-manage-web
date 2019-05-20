<template>
  <div>
    <v-card>
      <!-- 卡片的头部 -->
      <v-card-title>
        <v-btn color="primary">新增</v-btn>
        <!--空间隔离组件-->
        <v-spacer />
        <!--搜索框，与search属性关联-->
        <v-text-field label="输入关键字搜索" v-model="search" append-icon="search" hide-details/>
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
            <v-btn color="info">编辑</v-btn>
            <v-btn color="warning">删除</v-btn>
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
            totalBrands: 0, // 总条数
            brands: [], // 当前页品牌数据
            loading: true, // 是否在加载中
            pagination: {}, // 分页信息
            headers: [ // 头信息
              {text: 'id', align: 'center', value: 'id'},
              {text: '名称', align: 'center', value: 'name', sortable: false},
              {text: 'LOGO', align: 'center', value: 'image', sortable: false},
              {text: '首字母', align: 'center', value: 'letter'},
              {text: '操作', align: 'center', value: 'id', sortable: false}
            ]
          }
        },
        mounted(){ // 渲染后执行
          // 查询数据
          this.getDataFromServer();
        },
        methods:{
          getDataFromServer(){ // 从服务的加载数据的方法。
            // 伪造假数据
            const brands = [
              {
                "id": 2032,
                "name": "OPPO",
                "image": "http://gizchina.es/wp-content/uploads/2014/10/oppo-logo-1-1024x473.jpg",
                "letter": "O",
                "categories": null
              },
              {
                "id": 2033,
                "name": "飞利浦（PHILIPS）",
                "image": "http://img5.pcpop.com/ProductImages/0x0/0/210/000210093.jpg",
                "letter": "F",
                "categories": null
              },
              {
                "id": 2034,
                "name": "华为（HUAWEI）",
                "image": "http://ku.90sjimg.com/element_origin_min_pic/17/12/21/213ee5955f5ce4adedd2a1ce14a84ee6.jpg",
                "letter": "H",
                "categories": null
              },
              {
                "id": 2036,
                "name": "酷派（Coolpad）",
                "image": "http://bpic.588ku.com/element_origin_min_pic/17/12/29/5668e2fb9c14c8c27713642c66f37045.jpg",
                "letter": "K",
                "categories": null
              },
              {
                "id": 2037,
                "name": "魅族（MEIZU）",
                "image": "http://image0.lietou-static.com/img/54ae5cfc0cf2860fbba8700c02c.png",
                "letter": "M",
                "categories": null
              }
            ];
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
