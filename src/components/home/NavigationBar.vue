<template>
  <div>
    <div class="nav-bar-container">
      <div class="left-action-bar">
        <img src="@/assets/mmall.png" class="icon">
      </div>
      <el-menu :default-active="activeIndex" mode="horizontal" :router="true" class="nav-bar"
               text-color="#CCCCCC" background-color="#292A2D" active-text-color="#FFFFFF">
        <el-menu-item index="/">Mmall 商城首页</el-menu-item>
        <el-menu-item index="/cart">购物车</el-menu-item>
        <el-menu-item index="/warehouse" :disabled="!isAdministrator">商品库存</el-menu-item>
        <!-- <el-menu-item index="/comment">留言板</el-menu-item> -->
      </el-menu>
      <div class="right-action-bar">
        <div class="right-action">
          <UserInformation/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import UserInformation from './UserInformation'
import {mapGetters} from 'vuex'

export default {
  components: {
    UserInformation
  },
  data () {
    return {
      activeIndex: '/'
    }
  },
  computed: {
    ...mapGetters('user', ['isAdministrator'])
  },
  methods: {}
}
</script>

<style scoped>
  .icon {
    height: 40px;
    padding: 7px 0 0 20px;
    cursor: pointer;
  }

  .nav-bar-container {
    background-color: #292A2D;
    text-align: center;
    height: 60px;
  }

  .nav-bar {
    display: inline-block;
  }

  .left-action-bar {
    display: inline-block;
    float: left;
    height: 100%;
  }

  .right-action-bar {
    display: inline-block;
    float: right;
    height: 100%;
  }

  .right-action {
    padding: 9px 15px;
  }

  .right-action > i {
    margin-right: 10px;
    color: #ccc;
    font-size: 20px;
    line-height: 60px;
  }

  .right-action > i:hover {
    color: #fff;
  }

  a {
    color: rgb(204, 204, 204);
    text-decoration: none;
  }
</style>
