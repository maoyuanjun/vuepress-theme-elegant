<template>
    <div style="height:100%">
        <el-container class="main-container" :style="{backgroundColor: containerBgColor}">
            <!-- 侧边栏 -->
            <my-aside :isHide="isHide"></my-aside>
            <el-container class="container-warp">
                <!-- 头部栏 包括关闭和搜索组件 -->
                <my-header
                        @clickMenu="clickMenu"
                        :showIcon="isHide"
                >
                </my-header>
                <!-- 正文内容 -->
                <my-main
                        :isHide="isHide"
                        :content="content"
                ></my-main>
            </el-container>
            <go-top></go-top>
        </el-container>
        <my-footer
                :content="content"
                :isHide="isHide"
        ></my-footer>
        <div
                @click="close"
                class="overlay"
                :class="{'overlay--active': needOverlay}"
        ></div>
    </div>
</template>
<script>
    import themeStyle from '../style/index';
    import content from "imData/content.js";

    export default {
        name: "Layout",
        data() {
            return {
                isHide: false,
                needOverlay: false,
                content: content
            };
        },

        computed: {
            containerBgColor() {
                const style = this.$themeConfig.style || 'classical';
                return themeStyle[style].color;
            }
        },

        methods: {
            clickMenu() {
                this.isHide = !this.isHide;
                if (typeof window === "undefined") return;
                if (window.innerWidth <= 1190) {
                    this.needOverlay = !this.needOverlay;
                }
            },
            close() {
                this.needOverlay = !this.needOverlay;
                this.isHide = !this.isHide;
            }
        }
    };
</script>
<style lang="stylus" scoped>
    .main-container {
        min-height: 100%;
    }

    .container-warp {
        position: relative;
        overflow: hidden;
    }

    .overlay {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        pointer-events: none;
        transition: 0.5s cubic-bezier(0.25, 0.8, 0.5, 1);
        z-index: 35;
    }

    .overlay:before {
        position: absolute;
    }

    .overlay:before {
        background-color: #212121;
        bottom: 0;
        content: '';
        height: 100%;
        left: 0;
        opacity: 0;
        right: 0;
        top: 0;
        transition: inherit;
        transition-delay: 0.15s;
        width: 100%;
    }

    .overlay--active {
        pointer-events: auto;
        touch-action: none;
    }

    .overlay--active:before {
        opacity: 0.46;
    }

    .go-next {
        transform: rotateY(180deg) !important;
        right: 10px !important;
    }
</style>