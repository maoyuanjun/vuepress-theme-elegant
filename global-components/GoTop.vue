<template>
    <el-button
        @click="GoTop"
        v-show="!isPost"
        :class="{show: show}"
        type="primary"
        circle
        class="gotop-btn"
        :style="{backgroundColor: goTopBgColor}"
    >
        <i class="el-icon-arrow-up"></i>
    </el-button>
</template>
<script>

    import themeStyle from '../style/index';

    export default {
        name: "GoTop",
        data() {
            return {
                show: false
            };
        },
        computed: {
            goTopBgColor() {
                const style = this.$themeConfig.style || 'classical';
                return themeStyle[style].goTopBgColor;
            },
            isPost() {
                return this.$route.path.slice(1, 6) === "posts";
            }
        },
        mounted() {
            this.hasShow();
        },
        methods: {
            hasShow() {
                const _this = this;
                window.addEventListener("scroll", function (e) {
                    let h = _this.getScrollTop();
                    if (h > 400) {
                        _this.show = true;
                    } else {
                        _this.show = false;
                    }
                });
            },
            GoTop() {
                window.scrollTo({top: 0, behavior: "smooth"});
            },
            getScrollTop() {
                var scrollPos;
                if (typeof window === "undefined") return;
                if (window.pageYOffset) {
                    scrollPos = window.pageYOffset;
                } else if (document.compatMode && document.compatMode !== "BackCompat") {
                    scrollPos = document.documentElement.scrollTop;
                } else if (document.body) {
                    scrollPos = document.body.scrollTop;
                }
                return scrollPos;
            }
        }
    };
</script>
<style lang="scss" scoped>
    .gotop-btn {
        transition: 0.3s cubic-bezier(0.25, 0.8, 0.5, 1);
        position: fixed;
        right: 30px;
        bottom: 30px;
        z-index: 69;
        opacity: 0;
        transform: scale(0);
        box-shadow: 0 3px 5px -1px rgba(0, 0, 0, 0.2),
        0 6px 10px 0 rgba(0, 0, 0, 0.14), 0 1px 18px 0 rgba(0, 0, 0, 0.12);
        border: 1px solid transparent;
        i {
            font-size: 1.5em;
            font-weight: 600;
        }
    }
    .show {
        opacity: 1;
        transform: scale(1);
    }

    @media only screen and (max-width: 767px) {
        .gotop-btn {
            right: 15px;
            bottom: 10px;
        }
    }
</style>