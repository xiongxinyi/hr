<template>
  <div class="common-layout">
    <el-container>
      <el-header class="common-header flex-float">
        <div class="flex">
          <img class="logo" src="../../assets/logo1.jpg" alt="" />
          <h1 class="title">社招人员信息管理系统</h1>
        </div>
        <!-- 头像 -->
          <el-avatar style="position: relative; left: 620px" 
          shape="square" :size="50"> {{ name }} </el-avatar>
        <!-- 退出按钮 -->
        <el-button type="danger" @click="loginOut">退出登录</el-button>
      </el-header>

      <el-container>
        <el-aside class="common-aside" width="160px">
          <el-menu background-color="none" text-color="#fff" :router="true">

            <el-menu-item index="/application">
              <el-icon><List /></el-icon>
                <span>查询个人申请表</span>
              </el-menu-item>

              <el-menu-item index="/audit">
              <el-icon><Checked /></el-icon>
                <span>审批审核</span>
              </el-menu-item>


            <el-menu-item index="/checkEveryone">
              <el-icon><Avatar /></el-icon>
                <span>查看部门所有人</span>
            </el-menu-item>

          </el-menu>
        </el-aside>

        <el-main>
          <!--router-view-->
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>
<script>
import { useStore } from "vuex";
import { useRouter } from "vue-router";

export default {
  name: "layOut",
  setup() {
    const name = localStorage.getItem("name");
    const store = useStore();
    const router = useRouter();
    const loginOut = () => {
      localStorage.removeItem(
        "dept",
        "loginData",
        "usercode",
        "role",
        "name",
        "token"
      );
      localStorage.removeItem("loginData");
      localStorage.removeItem("usercode");
      localStorage.removeItem("role");
      localStorage.removeItem("name");
      localStorage.removeItem("token");
      store.commit("setUserInfo", {});
      router.push({
        path: "./login",
      });
    };
    return {
      loginOut,
      name,
    };
  },
};
</script>
<style>
.el-container {
  height: 100vh;
  overflow: hidden;
}
.avatar-container {
  position: relative;
}
.common-header {
  background: rgb(39, 45, 53);
  display: flex;
}
.common-aside {
  background: rgb(48, 55, 65);
}
.logo {
  width: 40px;
}
.title {
  color: #fff;
}
.el-main {
  background: #efefef;
}
</style>