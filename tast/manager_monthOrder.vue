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
        <el-collapse>
          <el-collapse-item
            name="1"
            v-for="(item, index) in allUserOrder"
            :key="index"
          >
            <template slot="title">
              <div class="title">
                <div class="item">
                  <span>订单编号:</span><span>{{ item.orderId }}</span>
                </div>
                <div class="item">
                  <span>用户名:</span><span>{{ item.userName }}</span>
                </div>
                <div class="item">
                  <span>总金额:</span><span>{{ item.totalPrice }}</span
                  >元
                </div>
                <div class="item">
                  <span>商品数量:</span><span>{{ item.totalQuantity }}</span>
                </div>
              </div>
            </template>
            <div class="good">
              <el-table
                :data="item.goods"
                width="100%"
                stripe
                border
                style="padding-bottom: 10px"
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
                <el-table-column align="left" label="换购商品" prop="goodName">
                </el-table-column>
                <el-table-column
                  align="left"
                  label="单价(元/件)"
                  prop="unitPrice"
                >
                </el-table-column>
                <el-table-column align="left" label="数量(件)" prop="count">
                </el-table-column>
                <el-table-column
                  align="left"
                  label="总价"
                  prop="singleTotalPrice"
                >
                </el-table-column>
              </el-table>
            </div>
          </el-collapse-item>
        </el-collapse>
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
              <!-- <span class="num">{{}}</span> -->
            </div>
            <div
              class="card"
              :class="beSelect === 2 ? 'on' : ''"
              @click="getOneTypeGoods(2, '日用品类')"
            >
              <span class="name">日用品类</span>
              <!-- <span class="num">{{}}</span> -->
            </div>
            <div
              class="card"
              :class="beSelect === 3 ? 'on' : ''"
              @click="getOneTypeGoods(3, '零食类')"
            >
              <span class="name">零食类</span>
              <!-- <span class="num">{{}}</span> -->
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
.leftBtn .on,
.goodsType .on {
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
.secondLevelMain .employeesOrders .title {
  display: flex;
  justify-content: space-between;
  padding-right: 30px;
}
.secondLevelMain .employeesOrders .title,
.secondLevelMain .employeesOrders .title span {
  color: #869bfa;
}
.secondLevelMain .employeesOrders .title .item:not(:last-child) {
}
.collapse-transition {
  -webkit-transition: 0s height, 0s padding-top, 0s padding-bottom;
  transition: 0s height, 0s padding-top, 0s padding-bottom;
}

.horizontal-collapse-transition {
  -webkit-transition: 0s width, 0s padding-left, 0s padding-right;
  transition: 0s width, 0s padding-left, 0s padding-right;
}

.horizontal-collapse-transition .el-submenu__title .el-submenu__icon-arrow {
  -webkit-transition: 0s;
  transition: 0s;
  opacity: 0;
}
</style>>

</style>
<script>
export default {
  data() {
    return {
      ruleFormData: [],
      ruleFormData2: [],
      showOrder: true,
      beSelect: 1,
      allUserOrder: [
        {
          orderId: "HG481",
          userName: "宋雨",
          totalPrice: 220,
          totalQuantity: 5,
          goods: [
            {
              goodName: "多力葵花籽油",
              unitPrice: 110,
              count: 2,
              singleTotalPrice: 220,
            },
          ],
        },
        {
          orderId: "HG482",
          userName: "方志勇",
          totalPrice: 220,
          totalQuantity: 8,
          goods: [
            {
              goodName: "芝麻糊",
              unitPrice: 11,
              count: 1,
              singleTotalPrice: 11,
            },
          ],
        },
        {
          orderId: "HG483",
          userName: "胡玲玲",
          totalPrice: 1100,
          totalQuantity: 10,
          goods: [
            {
              goodName: "",
              unitPrice: 110,
              count: 2,
              singleTotalPrice: 220,
            },
          ],
        },
      ],
    };
  },
  methods: {
    getOneTypeGoods(beSelect, typeName) {
      this.beSelect = beSelect;
    },
  },
  created() {
    console.log("子路由加载");
    this.$parent.isShowRouter = true;
  },
};
</script>