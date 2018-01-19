<template>
    <header class="header">
        <div class="nav_container">
            <div class="bg_white"></div>
            <nav class="navbar navbar-default" role="navigation" id="nav">
                    <div class="container-fluid"> 
                    <div class="navbar-header">
                        <button type="button" class="navbar-toggle" data-toggle="collapse"
                                data-target="#example-navbar-collapse">
                            <span class="sr-only">切换导航</span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                            <span class="icon-bar"></span>
                        </button>
                        <a class="navbar-brand" href="#">
                            <div class="search">
                                <input class="form-control" type="text" placeholder="找一找" v-model="text" @keydown.enter="search" />
                            </div>
                        </a>
                    </div>
                    <div class="collapse navbar-collapse" id="example-navbar-collapse">
                        <ul class="nav navbar-nav nav_link">
                            <li class="active">
                                <router-link to="/home" tag="a">Home</router-link>
                            </li>
                            <li>
                                <router-link to="/about" tag="a">about</router-link>
                            </li>
                            <li>
                                <router-link to="/contact" tag="a">something</router-link>
                            </li>
                            <li>
                                <router-link to="/articles" tag="a">Tags</router-link>
                            </li>
                        </ul>
                    </div>
                    </div>
                </nav>
        </div>
        <div class="col-sm-12 col-xs-12 banner_container">
            <img :src=headline.src alt="headerBg" title="headerBg"/>
            <div class="banner_text">
                    <p class="main_title">{{headline.title}}</p>
                    <p class="description">{{headline.description}}</p>
            </div>
        </div>
        </header>
    
</template>

<script>
import {mapState, mapActions} from 'vuex'
export default {
    data () {
        return {
            text: ''
        }
    },
    computed: mapState(['headline']),
    methods: {
        ...mapActions(['searchArticles']),
        search () {
            this.$router.push({name: 'SearchResult', params: {text: this.text}, hash: '#search'})
        }
    },
    watch: {
        $route () {
            this.text = ''
        }
    }
}
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
.nav_container{
    position: absolute;
    z-index: 100;
    width: 100%;
}

#nav{
    background: transparent;
    margin: 0;
    border: none;
    
    .navbar-brand{
        padding: 0;
    }
    .navbar-toggle{
        border:none;
        background: none;
        .icon-bar{
            background: #fff;
        }
    }
    .search{
        margin: 8px 0 8px 15px;
        .form-control{
            background: transparent;
            border-color:#fff;
            &::-ms-input-placeholder{
                color: #fff;
            }
            &::-webkit-input-placeholder{
                color: #fff;
            }
        }
    }
    .nav_link{
        li{
            a{
                color: #fff;
                font-weight:600;
                font-size:14px;
                text-transform:uppercase;
            }
        }
        .active{
            a{
                background:transparent;
            }
        }
    }
}
.banner_container{
    padding: 0;
    overflow: hidden;
    img{
        width:100%;
        border: none;
    }
    .banner_text{
        position: absolute;
        top:50%;
        left:50%;
        p{
            color:#fff;
            text-align: center;
        }
        .description{
            letter-spacing: 1px;
        }
    }
}
@media(min-width:768px){
    #nav{
        .nav_link{
            float: right;
        }
    }
    .banner_container{
        height: 450px;
        .banner_text{
            width: 385px;
            height: 162px;
            margin-left: -192.5px;
            margin-top: -81px;
            .main_title{
                font-size: 80px;
            }
            .description{
                font-size: 20px;
            }
        }
    }
}
@media(max-width:768px){
    #nav{
        .navbar-collapse{
            width: 150px;
            position: absolute;
            right:30px;
            background:#fff;
            li{
                a{
                    color: #777;
                }
            }
            
        }
    }
    .banner_container{
        height: 250px;
        img{
            height:100%;
        }
        .banner_text{
            width: 193px;
            height: 97px;
            margin-left: -96.5px;
            margin-top: -48.5px;
            .main_title{
                font-size: 40px;
            }
            .description{
                font-size: 14px;
            }
        }
    }
}
</style>
