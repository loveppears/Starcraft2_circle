<template>
    <div class="layout">
        <!--<Menu mode="horizontal" theme="dark">
            <div><a><img class="layout-logo" :src="imgPath"></img></a></div>
            <div class="layout-nav">
                <Menu-item name="1">
                    <router-link :to="{path: '/signup'}">
                        <div @click="changethat">注册</div>
                    </router-link>
                    
                </Menu-item>
                <Menu-item name="2">
                    登录
                </Menu-item>
                <Menu-item name="3">
                    关于
                </Menu-item>
            </div>
        </Menu>-->
        <div class="layout-content">
            <Row >
                <i-col span="17">
                    <div class="layout-content-main">
                        <Card>
                            <div class="segment">
                                <div class="selected items">
                                    <div class="item">
                                        <a href="/user/lita" class="ui spacing" style="width: 50px;">
                                        <img src="http://res.cloudinary.com/dwwn5mrou/image/upload/v1495804973/iwjvmrtwvbmddrslfncv.png">
                                        </a>
                                        <div class="top content spacing">
                                            <a class="header" href="/topic/1">Computed Properties and Watchers</a>
                                            <div class="meta">
                                            <span class="cinema">
                                                <a class="header" href="/user/1"></a>
                                                发布于9 天前●
                                                回复2●
                                                浏览8
                                            </span>
                                            </div>
                                        </div>
                                        <div class="middle spacing right floated">
                                            <div class="ui horizontal list">
                                            <div class="">
                                                <a class="" href="/user/lira">
                                                <img class="ui avatar image" style="width: 3em;height: 3em;" src="http://res.cloudinary.com/hezf/image/upload/v1467186691/vwuj8a3tpuqoy5fzuzlw.png">
                                                </a>
                                            </div>
                                            <div class="" style="width: 60px; margin: 0px;padding: 0px">
                                                <div class="content" style="font-size: smaller">9 天前</div>
                                            </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                </div>
                        </Card>
                         <Card>
                            <div class="segment">
                                <div class="selected items">
                                    <div class="item">
                                        <a href="/user/lita" class="ui spacing" style="width: 50px;">
                                        <img src="http://res.cloudinary.com/dwwn5mrou/image/upload/v1495804973/iwjvmrtwvbmddrslfncv.png">
                                        </a>
                                        <div class="top content spacing">
                                            <a class="header" href="/topic/1">Computed Properties and Watchers</a>
                                            <div class="meta">
                                            <span class="cinema">
                                                <a class="header" href="/user/1"></a>
                                                发布于9 天前●
                                                回复2●
                                                浏览8
                                            </span>
                                            </div>
                                        </div>
                                        <div class="middle spacing right floated">
                                            <div class="ui horizontal list">
                                            <div class="">
                                                <a class="" href="/user/lira">
                                                <img class="ui avatar image" style="width: 3em;height: 3em;" src="http://res.cloudinary.com/hezf/image/upload/v1467186691/vwuj8a3tpuqoy5fzuzlw.png">
                                                </a>
                                            </div>
                                            <div class="" style="width: 60px; margin: 0px;padding: 0px">
                                                <div class="content" style="font-size: smaller">9 天前</div>
                                            </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                </div>
                        </Card>
                    </div>
                </i-col>
                <i-col span="6" offset="1" class="layout-line">
                    <Menu active-name="1-2" width="auto" :open-names="['1']">
                        <Submenu name="1">
                            <template slot="title">
                                <Icon type="ios-navigate"></Icon>
                                导航一
                            </template>
                            <Menu-item name="1-1">选项 1</Menu-item>
                            <Menu-item name="1-2">选项 2</Menu-item>
                            <Menu-item name="1-3">选项 3</Menu-item>
                        </Submenu>
                        <Submenu name="2">
                            <template slot="title">
                                <Icon type="ios-keypad"></Icon>
                                导航二
                            </template>
                            <Menu-item name="2-1">选项 1</Menu-item>
                            <Menu-item name="2-2">选项 2</Menu-item>
                        </Submenu>
                        <Submenu name="3">
                            <template slot="title">
                                <Icon type="ios-analytics"></Icon>
                                导航三
                            </template>
                            <Menu-item name="3-1">选项 1</Menu-item>
                            <Menu-item name="3-2">选项 2</Menu-item>
                        </Submenu>
                    </Menu>
                </i-col>
            </Row>
        </div>
        <!--
        <my-modal :pmodal6="modal6" @closeD='closeDialog'></my-modal>
        -->
    </div>
</template>

<script>
// import MyModal from './dialog'
export default {
     components : {
        
     },
     data () {
      return {
         modal6: false
      }
    },
    methods : {
        test () {
            console.log(1212);
            this.axios.get('/api/fuck').then((response) => {
                console.log(response.data)
            }, (err) => {
                console.log(err)
            })
        },
        changethat () {
            alert(1212);
            this.modal6 = !this.modal6;
            console.log(this.modal6);
        },
        closeDialog () {
            this.modal6 = false;
        }
    }
}
</script>

<style scoped>
    .layout-assistant{
        width: 300px;
        margin: 0 auto;
        height: inherit;
    }
    .layout-breadcrumb{
        padding: 10px 15px 0;
    }
    .layout-content{
        min-height: 200px;
        margin: 15px;
        overflow: hidden;
        background: #fff;
        border-radius: 4px;
    }
    .layout-content-main{
        padding: 10px;
    }

    .layout-line {
        border-left: thin solid rgb(153,154,29);
    }

    /*0604*/
    .item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        flex-wrap: wrap;
        margin-bottom : -50px;
    }
    img {
        height : 60px;
    }
    .spacing {
        margin-bottom : 50px;
    }
    .layout-content-main {
        
    }
</style>