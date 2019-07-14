<template>
    <aside class="aside__top">
        <span
            class="iconfont icon-nav toggleNavCollapse"
            :class="{active:isSidebarNavCollapse}"
            @click="toggleNavCollapse"
        >
        </span>
        <el-breadcrumb separator="/">
            <transition-group name="breadcrumb">
                <!-- 防止面包屑导航出现 首页/首页， v-if="route.name!='home'" -->
                <el-breadcrumb-item
                    v-for="(route,i) in crumbList"
                    :key="route.name"
                    :to="{name:route.name}"
                    v-if="route.name!='home'"
                    :class="{'is-last-link':i==crumbList.length-1}"
                >
                    {{route.meta.name}}
                </el-breadcrumb-item>
            </transition-group>
        </el-breadcrumb>
    </aside>
</template>

<script>
import { mapState } from 'vuex'

export default {
    data() {
        return {}
    },
    computed: {
        ...mapState(['isSidebarNavCollapse', 'crumbList'])
    },
    methods: {
        toggleNavCollapse() {
            this.$store.commit('toggleNavCollapse')
        }
    }
}
</script>

<style lang="scss" scoped>
.aside__top {
    border-bottom: 1px solid #e5e5e5;
    height: 50px;
    line-height: 50px;
    position: relative;
    left: 0;
    top: 0;
    right: 0;
    background: #fff;
    z-index: 1000;
    transition: left 0.25s;
    .toggleNavCollapse {
        display: inline-block;
        margin-left: 8px;
        padding: 0 10px;
        font-size: 26px;
        vertical-align: middle;
        color: #333;
        cursor: pointer;
        transition: all 0.5s;
        &.active {
            transform: rotate(90deg);
        }
    }
}
</style>
