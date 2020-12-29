<template>
  <div class="monthOrder secondLevel">
    <div class="orderBtn">
      <div class="leftBtn">
        <span class="text">本月订单</span>
        <el-button
          @click="showOrder = false"
          :class="showOrder === false ? 'on' : ''"
          class="button1"
          type="text"
          >商品订单</el-button
        >
        <el-button
          @click="showOrder = true"
          :class="showOrder === true ? 'on' : ''"
          class="button2"
          type="text"
          >员工订单</el-button
        >
      </div>
      <div class="rightBtn">
        <el-button type="text"
          ><span><i class="iconfont icon-bar-sousuo"></i> 搜索</span></el-button
        >
        <el-button type="text"
          ><span><i class="iconfont icon-bar-daochu"></i> 导出</span></el-button
        >
      </div>
    </div>
    <div class="secondLevelMain">
      <div class="table employeesOrders" v-if="showOrder">
        <el-table
          :data="ruleFormData"
          width="100%"
          stripe
          border
          height="100%"
          :header-cell-style="{
            background: '#eef1fe',
            color: '#869bfa',
            borderBottom: '1px,solid #869bfa',
          }"
        >
          <el-table-column type="index" align="center" label="序号" width="50">
          </el-table-column>
          <el-table-column align="center" label="订单编号"> </el-table-column>
          <el-table-column align="center" label="名字"> </el-table-column>
          <el-table-column align="center" label="换购商品"> </el-table-column>
          <el-table-column align="center" label="数量"> </el-table-column>
          <el-table-column align="center" label="换购详情"> </el-table-column>
        </el-table>
      </div>

      <div v-else class="goodsOrder">
        <div class="goodsType">
          <div class="cards">
            <div
              class="card"
              :class="beSelect === 1 ? 'on' : ''"
              @click="getOneTypeGoods(1, '粮油类')"
            >
              <span class="name">粮油类</span>
              <span class="num">{{  }}</span>
            </div>
            <div
              class="card"
              :class="beSelect === 2 ? 'on' : ''"
              @click="getOneTypeGoods(2, '日用品类')"
            >
              <span class="name">日用品类</span>
              <span class="num">{{  }}</span>
            </div>
            <div
              class="card"
              :class="beSelect === 3 ? 'on' : ''"
              @click="getOneTypeGoods(3, '零食类')"
            >
              <span class="name">零食类</span>
              <span class="num">{{  }}</span>
            </div>
          </div>
        </div>
        <div class="goodsOrderDetails">
          <el-table
            :data="ruleFormData2"
            width="100%"
            stripe
            border
            height="100%"
            :header-cell-style="{
              background: '#eef1fe',
              color: '#869bfa',
              borderBottom: '1px,solid #869bfa',
            }"
          >
            <el-table-column
              type="index"
              align="center"
              label="序号"
              width="50"
            >
            </el-table-column>
            <el-table-column align="center" label="商品名称"> </el-table-column>
            <el-table-column align="center" label="数量"> </el-table-column>
          </el-table>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.leftBtn .on,.goodsType .on{
  background-color: #869bfa;
  color: #fff;
}
.leftBtn button {
  border: 1px #99aaf8 solid;
  padding: 5px 12px;
  border-radius: 16px;
}
.leftBtn .button1 {
  margin-right: 20px;
  margin-left: 0px;
}
.secondLevelMain .goodsOrder {
  width: 100%;
  display: flex;
}
.goodsOrder .goodsType {
  width: 220px;
}
.goodsOrder .goodsOrderDetails {
  flex: 1;
}
.goodsOrder .goodsType .cards {
    margin-right: 12px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    width: 250px;
    min-width: 250px;
    flex-wrap: wrap;
    align-content: flex-start;
}
.goodsOrder .goodsType .cards .card {
    display: flex;
    flex-direction: column;
    width: 80px;
    height: 80px;
    border: 1px solid #d7e3fe;
    border-radius: 10px;
    box-shadow: 1px 1px 12px 1px rgba(175, 188, 249, 0.47);
    justify-content: center;
    align-items: center;
    margin-right: 20px;
    margin-bottom: 20px;
    cursor: pointer;
}
</style>>

</style>
<script>
export default {
  data() {
    return {
      ruleFormData: [],
      ruleFormData2: [],
      showOrder: false,
      beSelect:1
    };
  },
  methods: {
      getOneTypeGoods(beSelect,typeName){
          this.beSelect=beSelect

      }
  },
  created() {
    console.log("子路由加载");
    this.$parent.isShowRouter = true;
  },
};
</script>