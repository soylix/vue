<template lang="html">
    <div class="box-container">
        <div class="swipe-container">
            <div class="item-container">
                <div class="content">
                    <div class="content-title">这里是标题</div>
                    <div class="desc">这里是简单描述
                        <span>2018-01-17</span>
                    </div>
                </div>
            </div>
            <div class="action">
                <span class="action-edit">编辑删除</span>
                <span class="action-delete">删除</span>
            </div>
        </div>
        <div class="swipe-container">
            <div class="item-container">
                <div class="content">
                    <div class="content-title">这里是标题</div>
                    <div class="desc">这里是简单描述
                        <span>2018-01-17</span>
                    </div>
                </div>
            </div>
            <div class="action">
                <span class="action-edit">编辑删除</span>
                <span class="action-delete">删除</span>
            </div>
        </div>
    </div>
</template>
<script>
import $ from 'jquery'
export default {
    data() {
            return {

            };
        },
        methods: {
            setSlide() {
                var vm = this;
                let expansion = false;
                let container = document.querySelectorAll(".item-container");
                for (var i = 0; i < container.length; i++) {
                    var x, y, X, Y, swipeX, swipeY;
                    let btnOffSetWidth = 0;
                    let itemMargin = 0;
                    // debugger
                    // if(expansion) {
                    //   $(container[i])[0].style.marginLeft = 0 +'px';
                    // }
                    container[i].addEventListener('touchstart', function(event) {
                        x = event.changedTouches[0].pageX;
                        y = event.changedTouches[0].pageY;
                        swipeX = true;
                        swipeY = true;
                        if (expansion) {
                            let nodes = $(this).parent().parent().find('.item-container');
                            if (!nodes) {
                                return;
                            }
                            if (nodes.length > 0) {
                                for (var i = 0; i < nodes.length; i++) {
                                    $(nodes[i])[0].style.marginLeft = 0 + 'px';
                                }
                            }
                        }
                    });
                    container[i].addEventListener('touchmove', function(event) {
                        // debugger;
                        btnOffSetWidth = $(event.currentTarget.parentNode).find('.action')[0].offsetWidth;
                        itemMargin = $(event.currentTarget)[0].offsetLeft;
                        X = event.changedTouches[0].pageX;
                        Y = event.changedTouches[0].pageY;
                        //左右滑动
                        if (Math.abs(X - x) - Math.abs(Y - y) > 0) {
                            event.stopPropagation();
                            if ((X - x) > 0 && Math.abs(itemMargin) > 0) {
                                event.preventDefault();
                                // if((Math.abs(itemMargin)-Math.abs(X-x)) > 0) {
                                //   $(event.currentTarget)[0].style.marginLeft = (Math.abs(itemMargin)-Math.abs(X-x)) +'px';
                                // } else {
                                $(event.currentTarget)[0].style.marginLeft = 0 + 'px';
                                expansion = false;
                                // }
                            }
                            if (x - X > 0) { //左滑展开
                                event.preventDefault();
                                // console.log('syt',container[i], vm,);
                                if (Math.abs(X - x) > btnOffSetWidth) {
                                    $(event.currentTarget)[0].style.marginLeft = -btnOffSetWidth + 'px';
                                } else {
                                    $(event.currentTarget)[0].style.marginLeft = -Math.abs(X - x) + 'px';
                                }
                                expansion = true;
                            }

                        }

                    })
                    container[i].addEventListener('touchend', function(event) {
                        if ((X - x) < 0) {
                            if (Math.abs(X - x) < btnOffSetWidth) {
                                $(event.currentTarget)[0].style.marginLeft = 0 + 'px';
                                expansion = false;
                            } else {
                                $(event.currentTarget)[0].style.marginLeft = -btnOffSetWidth + 'px';
                                expansion = true;
                            }
                        }

                    })
                }
            }
        },
        mounted() {
            this.setSlide();
        },
        created() {

        }
}
</script>
<style>
.box-container {
    width: 100%;
    /* height: 56px; */
    overflow: hidden;
}

.item-container {
    width: 100%;
    background-color: #fff;
    height: 56px;
    z-index: 1000;
    -webkit-transition: all 0.5s linear;
    transition: all 0.5s linear;
}

.content-title {
    font-size: 16px;
    color: #000;
    margin-bottom: 8px
}

.desc {
    font-size: 12px;
    color: #999
}

.action span {
    display: inline-block;
    padding: 16px;
    font-size: 17px;
}

.action-delete {
    background: #C95454;
}

.action-edit {
    background: #00BCD4;
}

.swipe-container {
    width: 100%;
    height: 56px;
    position: relative;
}

.swipe-container .action {
    color: #fff;
    font-size: 0;
    position: absolute;
    right: 0;
    top: 0;
    z-index: -100;
}
</style>
