<template>
  <div style="position: relative" :class="{navCollapsed:isSidebarNavCollapse}">
    <div class="head">
      <div class="box">
        <a class="logo" href="/dashboard">
          <img src="../../assets/image/Foxit-logo-white-100.png" alt="logo" />
        </a>
        <div class="aside__top--right">
          <div class="user-msg">
            <img class="user-img" :src="require('@/assets/image/avatar.png')" alt />
            <span class="user-name" style="color:white;font-size:14px">Welcome,{{msg}}</span>
            <el-dropdown trigger="click" placement="top">
              <span class="el-dropdown-link">
                <i class="el-icon-arrow-down el-icon--right" style="color:white"></i>
              </span>
              <el-dropdown-menu slot="dropdown" style="position:fixed">
                <el-dropdown-item>language</el-dropdown-item>
                <el-dropdown-item>版本切换</el-dropdown-item>
                <el-dropdown-item class="quit-system" @click="loginOut">loginOut</el-dropdown-item>
              </el-dropdown-menu>
            </el-dropdown>
          </div>
        </div>
      </div>
    </div>
    <sidebarNav class="sidebar" />
    <mainContent />
  </div>
</template>

<script>
import sidebarNav from './component/sidebar-nav'
import mainContent from './component/main-content/index'
import { mapState } from 'vuex'
export default {
    data() {
        return {
            msg: 'admin'
        }
    },
    computed: {
        ...mapState(['isSidebarNavCollapse'])
    },
    methods: {
        loginOut() {
            this.$store.commit('LOGIN_OUT')
            /* 防止切换角色时addRoutes重复添加路由导致出现警告 */
            window.location.reload()
        }
    },
    components: {
        sidebarNav,
        mainContent
    }
}
</script>

<style lang="scss" scoped>
.head {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10000;
  width: 100%;
  height: 50px;
  background-color: #ef705b;
}
.head .box {
  width: 100%;
  height: 45px;
  padding-top: 3px;
  background-color: #555;
}
.head .box .logo {
  padding-left: 20px;
}
.aside__top--right {
    position: absolute;
    right: 10px;
    top: 10px;
    bottom: 0px;
    > div {
        position: relative;
        display: inline-block;
        text-align: center;
        vertical-align: middle;
        margin-left: 10px;
        padding: 0 15px;
        cursor: pointer;
        &:hover::after {
            transform-origin: 0 0;
            transform: scaleX(1);
        }
        &:first-child:before {
            border: none;
        }
        &::after {
            content: '';
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
            height: 2px;
            background: #ef4747;
            transform: scaleX(0);
            transform-origin: right 0;
            transition: transform 0.5s;
        }
        &::before {
            content: '';
            position: absolute;
            height: 20px;
            top: 50%;
            left: -8px;
            margin-top: -10px;
            border-left: 1px solid #ccc;
        }
        &.user-msg {
            .user-img {
                width: 25px;
                height: 25px;
                vertical-align: middle;
            }
            .user-name {
                color: #758eb5;
                padding: 0 4px;
            }
        }
    }
}
.breadcrumb-enter,
.breadcrumb-leave-active {
    opacity: 0;
    transform: translateX(20px);
}

.breadcrumb-enter-active,
.breadcrumb-leave-active {
    transition: all 0.6s;
}

.breadcrumb-leave-active {
    position: absolute;
}
</style>
