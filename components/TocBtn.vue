<template>
  <span>
    <el-button
            @click="OpenToc"
            type="primary"
            circle
            class="toc-btn"
            :style="{backgroundColor: btnBgColor}"
    >
      <i class="iconfont icon-service-directory"></i>
    </el-button>
    <el-button
            @click="GoTop"
            :class="{show: show}"
            type="primary"
            circle
            class="gotop-btn"
            :style="{backgroundColor: btnBgColor}"
    >
      <i class="el-icon-arrow-up"></i>
    </el-button>
  </span>
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
        mounted() {
            this.hasShow();
        },
        computed: {
            btnBgColor() {
                const style = this.$themeConfig.style || 'classical';
                return themeStyle[style].goTopBgColor;
            }
        },
        methods: {
            OpenToc() {
                this.$emit("toc");
            },
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
    .gotop-btn,
    .toc-btn {
        position: fixed;
        right: 30px;
        bottom: 30px;
        z-index: 69;
        color: #fff;
        border: 1px solid transparent;
        box-shadow: 0 3px 5px -1px rgba(0, 0, 0, 0.2),
        0 6px 10px 0 rgba(0, 0, 0, 0.14), 0 1px 18px 0 rgba(0, 0, 0, 0.12);

        i {
            font-size: 1.5em;
            font-weight: 600;
        }
    }

    .toc-btn {
        transition: 0.3s cubic-bezier(0.25, 0.8, 0.5, 1);
        opacity: 1;
        transform: scale(1);
    }

    .gotop-btn {
        display: none;
        opacity: 0;
        transform: scale(0);
    }

    @media (min-width: 1190px) {
        .gotop-btn {
            display: inline-block;
        }
        .toc-btn {
            opacity: 0;
            transform: scale(0);
        }
    }

    .show {
        opacity: 1;
        transform: scale(1);
    }

    @media only screen and (max-width: 767px) {
      .gotop-btn,
      .toc-btn {
        right: 15px;
        bottom: 10px;
      }
    }
</style>