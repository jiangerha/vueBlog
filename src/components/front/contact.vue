<template>
    <div class="contact">
        <a href="#callMe" class="title animated bounceIn">
            <p class="headline" id="callMe">Contact me</p>
        </a>
        <div class="email animated fadeIn">
            <form class="form-horizontal" role="form">
                <div class="form-group">
                    <label for="email-theme" class="col-sm-2 control-label">邮件主题</label>
                    <div class="col-sm-10">
                        <input type="text" class="form-control" id="email-theme" placeholder="请输入邮件主题"  v-model="subject"/>
                    </div>
                </div>
                <div class="form-group">
                    <label for="email-address" class="col-sm-2 control-label">邮箱</label>
                    <div class="col-sm-10">
                        <input type="text" class="form-control" id="email-address" placeholder="请输入邮箱"  v-model="address"/>
                    </div>
                </div>
                <div class="form-group">
                    <label for="email-content" class="col-sm-2 control-label">邮件内容</label>
                    <div class="col-sm-10">
                        <textarea type="text" class="form-control" id="email-content" placeholder="请输入邮件内容" v-model="content"></textarea>
                    </div>
                </div>
                <div class="form-group">
                    <button type="button" class="sendEmail btn btn-primary btn-lg" @click="send" :disabled="sendFlag">
                        {{sendFlag ? '发送中...' : '确认'}}
                    </button>
                </div>
            </form>
            <!-- <input type="text" placeholder="请输入邮件主题" v-model="subject">
            <input type="text" placeholder=" 邮箱" v-model="address"/>
            <textarea placeholder=" 来唠唠嗑呗" spellcheck="false" v-model="content"></textarea> -->
           
        </div>
    </div>
</template>

<script>
import {mapMutations, mapActions} from 'vuex'
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
            content: 'Tags',
            src:'../../../static/something_bg.jpg',
            description:"This is Dora.",
            animation: 'animated rotateIn'
        })
    },
    methods: {
        ...mapMutations(['set_headline', 'set_dialog']),
        ...mapActions(['sendMail']),
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
    }

}

</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.contact {
    min-height: 30rem;
    padding: 2rem 1rem 2rem;
    .title {
        padding-top: 3.125rem;
        padding-bottom: 3.125rem;
        p {
            width: 13rem;
        }
    }
    .email {
        width: 40%;
        margin: 2rem auto 0;
        input {
            color: #666;
            font-size: 1.125rem;
            border: 0.125rem solid rgb(129, 216, 208);
            width: 70%;
            height: 34px;
            margin-bottom: 1.25rem;
            display: block;
            background: transparent;
            border:1px solid #d8d8d8;
            outline:none;
            text-indent:1em;
            border-radius:6px;
        }
        textarea {
            color: #666;
            font-size: 1.125rem;
            width: 100%;
            height: 15rem;
            resize: none;
            background: transparent;
            font-family: Georgia, "Microsoft YaHei", "微软雅黑",  STXihei, "华文细黑",  serif;
        }
        .sendEmail {
            width: 6.25rem;
            margin-top: 0.625rem;
            /* margin-left: calc(100% - 6.25rem); */
        }
        .form-group{
            &:last-child{
                text-align: right;
                margin-right:15px;
            }
        }
    }
}
p.headline {
    margin: 0 auto 0;
    text-align: center;
    color: #333;
    font-size: 24px;
    padding-bottom: 1.25rem;
}
@media screen and (max-width: 440px) {
    /*.title, .email {*/
        /*display: block !important;*/
    /*}*/
    .email {
        width: 100% !important;
    }
}
</style>
