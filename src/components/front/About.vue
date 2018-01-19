<template>
    <div class="container">
        <div class="row">
                <div class="about_container col-lg-8 col-lg-offset-1 col-md-8 col-md-offset-1 col-sm-12 col-xs-12">
                    <div class="">
                        <blockquote>
                            <p class="about_title">我就随便试试。<br/>I am just try.</p>
                        </blockquote>
                        <p>温情的东南风向北吹着，这风绵润而有力，空气便显得湿漉漉的，它很清爽，并没有沾湿我的衣服。右侧的荒野里有几棵粗壮的柳树，在霞光的怀抱里格外引人注目，它没有因年久时长而显出老气沧桑、一点没有，反而充满着朝气、充满了正的能量，青春不减、苍翠欲滴。它的地上根遍布四面八隅、错乱交横，每条根上都覆盖着一层墨绿色的苔藓，而且很密，三三两两的蚂蚁在懒散着爬动着，有种在高空俯视大地上的斑斑点点一般，只不过他们是动的、我是静的而已 。</p>
                    </div>
                </div>
                <rightSecction></rightSecction>
        </div>
    </div>
</template>

<script>
import {mapMutations} from 'vuex'
import rightSecction from './component/rightSection.vue'
export default {
    created () {
        this.set_headline({
            content: '关于我',
            title: 'About',
            src:'../../../static/about_bg.jpg',
            description:"This is Dora.",
            animation: 'animated bounce'
        })
    },
    methods: mapMutations(['set_headline']),
    components:{
        rightSecction
    }
}

</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.about_container{
    .about_title{
        color: rgb(128,128,128);
        font-weight:300;
        font-style:italic;
    }
}
@media(min-width:768px){
    .about_container{
        margin-top: 30px;
    }
}

</style>
