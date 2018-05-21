<template>
    <footer>
        <ul>
            <li><img src="../assets/images/a-home.png"></li>
            <li><img src="../assets/images/n-catergry.png"></li>
            <li><img src="../assets/images/n-find.png"></li>
            <li><img src="../assets/images/n-cart.png"></li>
            <li><img src="../assets/images/n-me.png"></li>
        </ul>
    </footer>
</template>

<script>
    export default {

    }
</script>

<style lang="less">
    footer {
        width: 100%;
        height: .98rem;
        background: #fff;
        border-top: 1px solid #cbcbcb;
        display: flex;
        align-items: center;
        justify-content: center;
        ul {
            display: flex;
            width: 100%;
            height: 100%;
            li {
                flex: 1;
                padding: 0 .12rem;
                img {
                    width: 100%;
                    height: 100%;
                }
            }
        }
    }
</style>