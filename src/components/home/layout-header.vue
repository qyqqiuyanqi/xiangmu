<template>
  <el-row type="flex" justify="space-between" class="layoutheader">
    <el-col :span="8" class="left">
      <i class="el-icon-s-fold icon"></i>
      <span>江苏传智播客教育科技股份有限公司</span>
    </el-col>
    <el-col :span="3" class="right" float:right>
      <img :src="userinfo.photo ? userinfo.photo : defaultImg" alt />
      <el-dropdown trigger="click" @command="handleCommand">
        <span class="el-dropdown-link">
          {{userinfo.name}}
          <i class="el-icon-arrow-down el-icon--right"></i>
        </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item command="a">用户信息</el-dropdown-item>
          <el-dropdown-item command="b">git地址</el-dropdown-item>
          <el-dropdown-item command="c">退出</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </el-col>
  </el-row>
</template>

<script>
export default {
  data () {
    return {
      userinfo: {},
      defaultImg: require('../../assets/img/avatar.jpg')
    }
  },
  methods: {
    getUserInfo () {
      // let token = window.localStorage.getItem('user-token');
      // console.log(token)
      this.$axios({
        url: '/user/profile'
        // headers: {'Authorization': "Bearer " + token}
      }).then(res => {
        // console.log(res)
        this.userinfo = res.data
        // console.log(this.userinfo)
      })
    },
    handleCommand (command) {
      if (command === 'a') {
        // 用户信息
      } else if (command === 'b') {
        window.location.href = 'https://github.com/qyqqiuyanqi/xiangmu.git'
      } else {
        // 清除缓存
        window.localStorage.clear()
        this.$router.push('/login')
      }
    }
  },
  created () {
    this.getUserInfo()
  }
}
</script>

<style lang="less" scoped>
.layoutheader {
  padding: 8px 0;
  // background-color: pink;
  .left {
    display: flex;
    align-items: center;
    font-size: 16px;
    .icon {
      font-size: 22px;
      margin: 0 5px;
    }
  }
  .right {
    display: flex;
    align-items: center;
    img {
      border-radius: 50%;
      width: 40px;
      height: 40px;
      margin-right: 8px;
    }
  }
}
</style>
