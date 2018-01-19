<template>
    <div class="container">
        <div class="row">
                <div class="col-lg-8 col-lg-offset-1 col-md-8 col-md-offset-1 col-sm-12 col-xs-12">
                            <div class="article_list">
                                <div v-for="(article, index) in reducedArticles" class="article_item">
                                    <div class="">
                                        <router-link :to="{name: 'article', params: {id: article.aid, index: index, page: 1}, hash: '#article'}" tag="h2" exact class="article_title">{{article.title}}</router-link>
                                        <!-- <span class="commentNumber"><i class="iconfont icon-huifu"></i>{{article.comment_n}}</span> -->
                                    </div>
                                    <p class="article_content">{{article.content}}</p>
                                    <!-- <router-link :to="{name: 'article', params: {id: article.aid, index: index, page: 1}, hash: '#article'}" tag="button" exact><span>Read More</span></router-link> -->
                                    <span class="article_time">{{article.date | toDate}}</span>
                                    <hr>
                                </div>
                            </div>
                </div>
                <rightSecction></rightSecction>
        </div>
    </div>
    
</template>

<script>
import {mapMutations, mapActions, mapGetters}   from 'vuex'
import rightSecction from './component/rightSection.vue'
export default {
    data () {
        return {
            subject: '',
            address: '',
            content: '',
            sendFlag: false
        }
    },
    created () {
        this.set_headline({
            title: 'Dore Blog',
            src:'../../../static/header_bg.jpg',
            description:'我就随便试试',
            animation: 'animated bounceIn'
        })
        this.getAllArticles({page: 1, limit: 5})
    },
    computed: {
        ...mapGetters(['reducedArticles'])
    },
    methods: {
        ...mapMutations(['set_headline', 'set_dialog']),
        ...mapActions(['getAllArticles', 'sendMail']),
        send () {
            const re = /^[\w_-]+@[\w_-]+\.[\w\\.]+$/
            if (!this.subject || !this.content) {
                this.set_dialog({
                    info: '还有选项没填(⊙o⊙)？',
                    hasTwoBtn: false,
                    show: true
                })
                return
            } else if (!re.test(this.address)) {
                this.set_dialog({
                    info: '请正确填写邮箱地址',
                    hasTwoBtn: false,
                    show: true
                })
                return
            }
            this.sendFlag = true
            this.sendMail({
                subject: this.subject,
                address: this.address,
                content: this.content
            }).then(() => {
                this.subject = ''
                this.content = ''
                this.address = ''
                this.sendFlag = false
            }).catch(() => {
                this.sendFlag = false
                this.set_dialog({
                    info: 'sorry, 邮件发送失败，请重新发送',
                    hasTwoBtn: false,
                    show: true
                })
            })
        }
    },
    components:{
        rightSecction
    }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.article_list{
    .article_item{
        .article_title{
            font-size: 21px;
            line-height: 1.3;
            margin-top: 30px;
            margin-bottom: 8px;
            cursor: pointer;
            &:hover{
                color: #0085a1;
            }
        }
        .article_content{
            color: #a3a3a3;
            font-size: 14px;
            letter-spacing: 1px;
        }
        .article_time{
            font-family: Lora,'Times New Roman',serif;
            color: #ccc;
            font-size: 16px;
            font-style: italic;
            margin-top: 0;
        }
    }
}
.section_title{
    color: #ccc;
    text-decoration:none;
    text-transform: uppercase;
}
.tags_container{
    .tags{
        a{
            display: inline-block;
            border: 1px solid rgba(255,255,255,.8);
            border-radius: 999em;
            padding: 0 10px;
            color: #bfbfbf;
            line-height: 24px;
            font-size: 12px;
            text-decoration: none;
            margin: 0 1px;
            margin-bottom: 6px;
            border-color: #bfbfbf;
            &:hover{
                color: #0085a1;
                border-color: #0085a1;
            }
        }
    }
}
@media(min-width:768px){
    .tags a{
        margin-right: 5px;
    }
}
.info_container{
    .some_info{
        img{
            width: 80%;
            margin-bottom:20px;
        }
        p{
            color: #ccc;
        }
    }
}
</style>
