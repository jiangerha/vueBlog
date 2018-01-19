<template>
    <div class="col-lg-3 col-lg-offset-0 col-md-3 col-md-offset-0 col-sm-12 col-xs-12 sidebar-container">
                    <section>
                        <div class="tags_container">
                            <hr class="hidden-sm hidden-xs">
                            <h5>
                                <a class="section_title" href="./contact">FEATURED TAGS</a>
                            </h5>
                            <div class="tags">
                                <a href="javascript:;">知乎</a>
                                <a href="javascript:;">Andriod</a>
                                <a href="javascript:;">前端开发</a>
                                <a href="javascript:;">知乎</a>
                                <a href="javascript:;">OS</a>
                                <a href="javascript:;">前端开发</a>
                                <a href="javascript:;">javascript</a>
                                <a href="javascript:;">Andriod</a>
                                <a href="javascript:;">前端开发</a>
                                <a href="javascript:;">知乎</a>
                                <a href="javascript:;">OS</a>
                                <a href="javascript:;">前端开发</a>
                                <a href="javascript:;">javascript</a>
                                <a href="javascript:;">Andriod</a>
                            </div>
                        </div>
                    </section>
                    <section class="visible-md visible-lg">
                        <div class="info_container">
                            <hr>
                            <h5>
                                <a class="section_title" href="./contact">about me</a>
                            </h5>
                            <div class="some_info">
                                <img src="../../../../static/dora.jpg"/>
                                <p>是的<br/>我就随便试试。</p>
                            </div>
                        </div>
                    </section>
                </div>
</template>
<style lang="scss" scoped>
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
