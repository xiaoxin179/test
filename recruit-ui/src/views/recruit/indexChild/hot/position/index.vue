<template>
  <!--    热门-->
  <div class="wrapper">
    <el-divider><h1>热门职位</h1></el-divider>
    <el-row :gutter="12">
      <el-col v-for="position in positionList" :span="8" style="height: 160px;">
        <el-card shadow="hover">
          <div slot="header" class="clearfix">
            <router-link :to="'/recruit/f/detail/'+position.id">{{ position.name }}</router-link>
            <el-button style="float: right; padding: 3px 0" type="text">{{ position.salaryDown }} - {{ position.salaryUp }}</el-button>
            <p>
              <span>{{ position.workCity}}</span>
              <el-tag size="mini">{{ position.category.parentCategory.categoryName }}</el-tag>
              <el-tag size="mini">{{ position.category.categoryName }}</el-tag>
            </p>
          </div>
          <el-row :gutter="12">
            <el-col :span="2">
              <img :src="position.company.logo" alt="">
            </el-col>
            <el-col :span="18">{{position.company.name}}</el-col>
          </el-row>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import { listInfo } from '@/api/recruit/company/info'
import { listPosition } from '@/api/recruit/position'

export default {
  name: 'Position',
  data(){
    return{
      // 查询参数
      queryParams: {
        pageNum: 1,
        pageSize: 10
      },
      positionList:[],
    }
  },
  methods:{
    listPosition(){
      listPosition(this.queryParams).then(response => {
        this.positionList = response.rows;
      });
    }
  },
  created() {
    this.listPosition()
  }
}
</script>

<style scoped>
.wrapper {
  margin: 40px 0 40px;
}
.el-card {
  margin-bottom: 10px;
}
img {
  width: 100%;
}
p span {
  font-size: 13px;
  color: #8d92a1;
}
p span,.el-tag {
  margin-right: 10px;
}
</style>
