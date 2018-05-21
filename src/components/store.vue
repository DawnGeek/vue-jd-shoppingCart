<template>
    <div class="store">

        <div class="title">
            <input
                type="checkbox"
                v-model="data.storeFlag"
                @click="selectFn" >
            <b>{{data.storeName}}</b>
        </div>
        <div class="product" v-for="(area, index) in data.product" :key="index">
            <input
                type="checkbox"
                v-model="area.pitch"
                @click="checkFn(index)">
            <div class="imgBox">
            </div>
            <div class="content">
                <p class="name">{{area.name}}</p>
                <div class="msg">{{area.msg}}</div>
                <div class="price">
                    <span>￥<b>{{area.price}}</b>.00</span>
                    <div class="bottonBox">
                        <button @click="sub(index)">-</button>
                        <span>{{area.count}}</span>
                        <button @click="plus(index)">+</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                flagCount: 0
            }
        },
        props: {
            data: {
                type: Object,
                default: {}
            }
        },
       methods: {
            sub(index) {
                if(!this.data.product[index].count) {
                    return false;
                }
                this.data.product[index].count--;
                this.$emit('listen');
            },
            plus(index) {
                this.data.product[index].count++;
                this.$emit('listen');
            },
            checkFn(index) {
                this.data.product[index].pitch = !this.data.product[index].pitch;
                this.flagCount = 0;
                this.data.product.forEach(v => {
                    if(v.pitch) {
                        this.flagCount++;
                    }
                });
                console.log(this.flagCount, this.data.product.length);
                if(this.flagCount == this.data.product.length) {
                    this.data.storeFlag = true;
                } else {
                    this.data.storeFlag = false;
                };
                this.$emit('listen');
            },
            selectFn() {
                this.data.storeFlag = !this.data.storeFlag;
                if(this.data.storeFlag) {
                    this.data.product.forEach(v => {
                        v.pitch = true;
                    });
                } else {
                    this.data.product.forEach(v => {
                        v.pitch = false;
                    });
                };
                this.$emit('listen');
            }
        }
    }
</script>

<style lang="less">
    .store {
        margin-top: .2rem;
        border-top: 1px solid #e3e5e9;
        border-bottom: 1px solid #e3e5e9;
        .title {
            width: 100%;
            height: .9rem;
            background: #fafafa;
            display: flex;
            align-items: center;
            padding-left: .24rem;
            b {
                margin-left: .26rem;
                color: #666;
            }
        }
        .product {
            width: 100%;
            height: 2.2rem;
            background: #fff;
            display: flex;
            align-items: center;
            padding-left: .24rem;
            .imgBox {
                width: 1.86rem;
                height: 1.86rem;
                background: #ccc;
                margin-left: .24rem;
                border-radius: 6px;
                overflow: hidden;
                img {
                    width: 100%;
                    height: 100%;
                }
            }
            .content {
                flex: 1;
                height: 1.6rem;
                margin-left: .24rem;
                .name {
                    width: 100%;
                }
                .msg {
                    width: 100%;
                    line-height: .4rem;
                    font-size: .22rem;
                    color: #81838e;
                }
                .price {
                    width: 100%;
                    padding-right: .24rem;
                    display: flex;
                    justify-content: space-between;
                    margin-top: .46rem;
                    &>span {
                        font-size: .26rem;
                        color: red;
                        b {
                            font-size: .34rem;
                        }
                    }
                    .bottonBox {
                        display: flex;
                        button {
                            width: .56rem;
                            height: .56rem;
                            color: #252528;
                            background: #fff;
                            border: none;
                            border: 1px solid #cfcfcf;
                            outline: none;
                        }
                        span {
                            width: .8rem;
                            height: .56rem;
                            border-top: 1px solid #cfcfcf;
                            border-bottom: 1px solid #cfcfcf;
                            display: block;
                            text-align: center;
                            line-height: .56rem;
                        }
                    }
                }
            }
        }
    }
</style>