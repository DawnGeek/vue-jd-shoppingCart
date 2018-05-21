<template>
    <main>
        <store-bar
            v-for="(item, index) in data"
            :data="item"
            @listen="calculate"
        />
        <div class="all">
            <input
                type="checkbox"
                @click="selectAll"
                id="allselect"/>
            <label for="allselect">全选</label>
            <div class="total">合计￥: <span>{{allPrice}}</span></div>
            <span class="go">结算({{allCount}})</span>
        </div>
    </main>
</template>

<script>
    import axios from 'axios';
    import storeBar from './store';
    export default {
        data() {
            return {
                data: null,
                allFlag: false,
                allPrice: 0,
                allCount: 0,
                selectCount: 0
            }
        },
        methods: {
            selectAll() {
                this.allFlag = !this.allFlag;
                if(this.allFlag) {
                    this.data.forEach(v => {
                        v.storeFlag = true;
                        v.product.forEach(a => {
                            a.pitch = true;
                        })
                    });
                } else {
                    this.data.forEach(v => {
                        v.storeFlag = false;
                        v.product.forEach(a => {
                            a.pitch = false;
                        });
                    });
                };
                this.selectCount = 0;
                this.calculate();
            },
            calculate() {
                this.allPrice = 0;
                this.allCount = 0;
                this.data.forEach(v => {
                    v.product.forEach(a => {
                        if(a.pitch) {
                            this.allPrice += a.price * a.count;
                            this.allCount += a.count;
                        }
                    });
                });
            }
        },
        mounted() {
            axios.get('api').then(res => {
                this.data = res.data.data;
            })
        },
        components: {
            storeBar
        }
    }
</script>

<style lang="less">
    main {
        position: relative;
        flex: 1;
        overflow-y: scroll;
        background: #f0f2f5;
        .all {
            position: absolute;
            left: 0;
            bottom: 0;
            display: flex;
            align-items: center;
            width: 100%;
            height: 1rem;
            background: #fff;
            border-top: 1px solid #dedede;
            padding-left: .24rem;
            .total {
                margin-left: .24rem;
            }
            .go {
                position: absolute;
                display: block;
                right: 0;
                top: 0;
                width: 2.4rem;
                height: 100%;
                text-align: center;
                line-height: 1rem;
                color: #fff;
                background: red;
            }
        }
    }
</style>