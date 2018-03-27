<template>
<div class="dialog">
    <!-- <div class="modal" id="reminder" tabindex="-1" role="dialog" aria-labelledby="reminderLabel" aria-hidden="true">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <button type="button" class="close" data-dismiss="modal" aria-hidden="true"  @click="close">
                        &times;
                    </button>
                        <h4 class="modal-title" id="reminderLabel">提示</h4>
                    </div>
                    <div class="modal-body">{{dialog.info}}</div>
                    <div class="modal-footer">
                        <button class="sure btn btn-primary btn-md" @click="confirm">确定</button>
                        <button type="button" class="cancel btn btn-default"  v-if="dialog.hasTwoBtn" @click="cancel">取消</button>
                    </div>
                </div>
            </div>
        </div> -->
        
    <div class="center">
        <div class="modal-header">
            <h4 class="modal-title" id="reminderLabel">提示</h4>
            <i  @click="close">&times;</i>
        </div>
        <div class="modal-content">
            {{dialog.info}}
        </div>
        <div class="modal-footer">
            <button class="sure btn btn-primary btn-md" @click="confirm">确定</button>
            <button type="button" class="cancel btn btn-default"  v-if="dialog.hasTwoBtn" @click="cancel">取消</button> 
        </div>
        <!-- <div class="choice">
        <button class="sure btn btn-primary btn-md" @click="confirm">确定</button>
        <button class="cancel btn btn-default" v-if="dialog.hasTwoBtn" @click="cancel">取消</button>
        </div> -->
    </div>
</div>
</template>

<script>
import {mapState, mapMutations}   from 'vuex'
export default {
    computed: {
        ...mapState(['dialog'])
    },
    mounted(){
        
    },
    methods: {
        ...mapMutations(['set_dialog']),
        close () {
            this.set_dialog({
                info: '',
                show: false
            })
        },
        confirm () {
            this.dialog.show = false
            this.dialog.resolveFn()
        },
        cancel () {
            this.dialog.show = false
            this.dialog.rejectFn()
        }
    }
}

</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.dialog {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: rgba(2, 2, 2, 0.8);
    z-index: 10;
    div.center {
        position: absolute;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        width: 30%;
        height: 20%;
        max-width:35%;
        overflow: auto;
        margin: auto;
        background: #fff;
        border-radius: 0.5rem;
        i {
            position: absolute;
            top: 1rem;
            right: 1rem;
            color: #333;
            font-size: 24px;
            cursor: pointer;
            &:hover {
                color: #666;
             }
        }
    }
}
.modal-content{
    padding: 15px 10px;
    border: none;
    box-shadow: none;
}
@media screen and (max-width: 440px) {
    .center {
        width: 90% !important;
        height: 35% !important;
    }
}
</style>
