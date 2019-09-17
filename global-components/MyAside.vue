<template>
    <el-aside
            class="menu"
            width="auto"
            :class="{ menuHide: isHide }"
    >
        <el-menu
                @select="select"
                :default-active="$route.path.slice(0, 7)"
                active-text-color="#3f51b5"
                class="menu-wrap"
        >
            <!-- 个人基本信息 -->
            <li>
                <div
                        class="brand-wrap"
                        :style="{backgroundImage : `url(${$withBase($themeConfig.brand || '')})`}"
                >
                    <div class="brand">
                        <router-link
                                to="/"
                                class="avatar waves-effect waves-circle waves-light"
                        >
                            <img :src="$withBase($themeConfig.avatar || '')">
                        </router-link>
                        <div class="introduce">
                            <div class="nickname">{{$themeConfig.author || '欢迎光临'}}</div>
                            <a
                                    :title="$themeConfig.email || '没有email'"
                                    class="mail"
                            >{{$themeConfig.email || '没有email'}}</a>
                        </div>
                    </div>
                </div>
            </li>
            <!-- 菜单信息 -->
            <el-menu-item index="/">
                <span class="item-split-wrap"></span>
                <i class="iconfont icon-home"></i>
                <span
                        class="item-title"
                        slot="title"
                >{{$themeConfig.menus.home || '主页'}}</span>
            </el-menu-item>
            <el-menu-item index="/tags/">
                <span class="item-split-wrap"></span>
                <i class="iconfont icon-biaoqian"></i>
                <span
                        class="item-title"
                        slot="title"
                >{{$themeConfig.menus.tags || '标签分类'}}</span>
            </el-menu-item>
            <el-menu-item index="/all/">
                <span class="item-split-wrap"></span>
                <i class="iconfont icon-wenzhang"></i>
                <span
                        class="item-title"
                        slot="title"
                >{{$themeConfig.menus.all || '时间归档'}}</span>
            </el-menu-item>
            <el-menu-item
                    index="/github/"
                    v-if="$themeConfig.github"
            >
                <span class="item-split-wrap"></span>
                <i class="iconfont icon-github"></i>
                <span
                        class="item-title"
                        slot="title"
                >{{$themeConfig.menus.github || 'GitHub'}}</span>
            </el-menu-item>
            <el-menu-item index="/about/">
                <span class="item-split-wrap"></span>
                <i class="iconfont icon-aboutme"></i>
                <span
                        class="item-title"
                        slot="title"
                >{{$themeConfig.menus.about || '自我介绍'}}</span>
            </el-menu-item>

        </el-menu>
    </el-aside>
</template>
<script>
    export default {
        name: "Aside",
        props: {
            isHide: {
                type: Boolean,
                default: false
            }
        },
        methods: {
            select(key) {
                if (key === "/github/") {
                    window.open(this.$themeConfig.github);
                } else {
                    this.$router.push(key);
                }
            }
        }
    };
</script>
<style lang="stylus" scoped>
    .el-menu {
        border-right: none;
    }

    .el-menu-item.is-active {
        background-color: #ECEEF8;
    }

    .el-menu-item:hover {
        color: #3f51b5;
        i {
            color: #3f51b5;
        }
    }

    .iconfont {
        color: #909399;
        margin-right: 19px;
        margin-left: 4px;
        width: 24px;
        text-align: center;
        font-size: 28px;
        vertical-align: middle;
        display: inline-block;
    }

    .menuHide .iconfont {
        margin-left: -5px;
        transition: 0.5s ease-in-out;
    }

    .menu {
        position: fixed;
        top: 0;
        left: 0;
        bottom: 0;
        z-index: 66;
        min-height: 100%;
        background: #fff;
        will-change: transform, -webkit-transform;
        transition: 0.2s ease-in-out;
        /*border 1px solid red;*/
    }

    .menuHide .menu-wrap {
        width: 60px;
    }

    .menu-wrap {
        width: 240px;
        transition: 0.2s ease-in-out;
    }

    .menu .brand-wrap {
        height 240px;
        /*border: 1px solid red;*/
        background-size: 100% 100%;
        background-repeat: no-repeat;
    }

    .menu .brand {
        /*padding: 41px 24px 24px;*/
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        transition: 0.2s ease-in-out;
    }

    .menuHide .brand {
        padding: 8px 4px;
        background: #fff;
    }

    .menu .avatar {
        /*border 1px solid red;*/
        transition: 0.2s ease-in-out;
        width: 78px;
        height: 78px;
        margin-top: 44px;
        /*border: 2px solid #fff;*/
        border-radius: 50%;
        overflow: hidden;
    }

    .menuHide .avatar {
        width: 48px;
        height: 48px;
    }

    .menu .avatar img {
        width: 100%;
        height: 100%;
    }

    .menu .introduce {
        display: flex;
        flex-direction: column;
        align-items: center;
        /*border: 1px solid blue;*/
        margin: 1em 0 0;
        margin-top: 16px;
        color: #1e1e1e;
        font-size: 16px;
        transition: 0.2s ease-in-out;
    }

    .menu .mail {
        display: inline-block;
        padding-top: 4px;
        color: #98989f;
        font-size: 12px;
    }

    .menuHide .introduce, .menuHide .item-title, .menuHide .item-split-wrap {
        display: none;
    }

    .menuHide .iconfont {
        margin-left: 12px !important;
    }

    .el-menu-item {
        /*border 1px solid blue;*/
        padding: 0 !important;
    }

    .el-menu-item.is-active{
        background-color: #ffffff !important;
        color: #5F4141 !important;
    }

    .el-menu-item.is-active .item-split-wrap {
        visibility: visible;
    }

    .el-menu-item {
        color: #98989F;
    }

    .el-menu-item:hover, .el-menu-item:focus {
        color: #5F4141 !important;
        background-color: #ffffff !important;
    }

    .el-menu-item i {
        margin-left: 20px;
    }

    .el-menu-item:hover i {
        color: #5F4141 !important;
    }

    .item-title {
        font-size: 16px;
    }

    .item-split-wrap {
        visibility: hidden;
        padding: 8px 2px;
        background-color: #5F4141;
    }

    @media (max-width: 1190px) {
        .menu {
            transform: translate(-100%, 0px);
        }

        .menuHide.menu {
            transform: translate(0, 0px);
        }

        .menuHide .menu-wrap {
            width: 240px;
        }

        .menuHide .introduce, .menuHide .item-title {
            display: inline-block;
        }

        .menuHide .avatar {
            width: 80px;
            height: 80px;
        }

        .menuHide .brand {
            padding: 41px 24px 24px;
            background-color #ffffff;
        }

        .menuHide .iconfont {
            margin-left: 4px;
        }
    }
</style>