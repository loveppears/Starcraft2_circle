<template>
    <div class="layout">
        <Menu mode="horizontal" theme="dark">
          <div class="img-position">
              <router-link :to="{path: '/'}"><img class="layout-logo" :src="imgPath"></img></router-link>
          </div>
          <div class="layout-nav">
            <Menu-item name="1" v-show='Object.keys(userInfo).length === 0' class="menu-align">
                <router-link :to="{path: '/signup'}">
                    注册
                </router-link>
            </Menu-item>
            <Menu-item name="2" v-show='Object.keys(userInfo).length === 0'>
                <router-link :to="{path: '/signin'}">
                    登录
                </router-link>
            </Menu-item>
            <Menu-item name="2">
              <template v-if="Object.keys(userInfo).length > 0">
                <router-link :to="{name: 'profile', params: { userid: userInfo.name}}">
                    {{userInfo.name}}
                </router-link>
               </template>
            </Menu-item>
            <Menu-item name="3">
                <router-link :to="{path: '/new'}">
                    关于
                </router-link>
            </Menu-item>
            <Menu-item name="3" >
                    <div @click="signOut()" v-if="Object.keys(userInfo).length > 0">退出</div>
            </Menu-item>
          </div>
        </Menu>
        <div class="layout-content">
            <Row >
                <i-col span="14" offset="2">
                  <transition name = 'fade'>
                    <router-view></router-view>
                  </transition>
                    <div class="layout-content-main" v-show="this.$route.path === '/'">
                    <template v-for="item in topics">
                        <Card>
                            <div class="segment">
                                <div class="selected items">
                                    <div class="item">
                                        <router-link :to="{name: 'profile', params: { userid: item.user_id}}" class="spacing">
                                            <img :src="item.avatarUrl">
                                        </router-link>
                                        <div class="top content spacing">
                                            <router-link :to="{name: 'article', params: { user: item.user_id, uid: item._id}}" class="header">
                                                {{item.title}}
                                            </router-link>
                                            <div class="meta">
                                            <span class="cinema">
                                                发布于{{convertTime(item.create_time)}} 天前●
                                                回复{{item.reply_count}}●
                                                浏览{{item.pv}}
                                            </span>
                                            </div>
                                        </div>
                                        <div class="middle spacing right floated">
                                            <div class="ui horizontal list">
                                            <div class="">
                                                 <router-link :to="{name: 'profile', params: { userid: item.user_id}}" class="spacing">
                                                    <img :src="item.avatarUrl" class="ui avatar image" style="width: 3em;height: 3em;" >
                                                </router-link>
                                            </div>
                                            <div>
                                                <div class="content" style="font-size: smaller">{{convertTime(item.create_time)}} 天前</div>
                                            </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                </div>
                        </Card>
                        </template>
                    </div>
                </i-col>
                <i-col span="5" offset="1" class="layout-line">
                 <template v-if="Object.keys(userInfo).length > 0">
                  <profile :profile="userInfo"></profile>
                  <topic :profile="userInfo" :titles="titles" @article="toggleArticle"></topic>
                 </template>
                  <div class="demo-spin-container" v-show="!userInfo">
                     <Spin fix size="large"></Spin>
                  </div>
                    <match></match>
                </i-col>
            </Row>
        </div>
        <div class="layout-copy">
          2011-2017 &copy; Brain-fucking
        </div>
    </div>
</template>

<script>
import Profile from './sidebars/profile'
import Topic from './sidebars/topics'
import Match from './sidebars/matches'
import moment from 'moment'
export default {
     components : {
        Profile,
        Topic,
        Match
     },
    created(){
      this.getUserInfo();
    },
     data () {
      return {
         imgPath : require('../assets/logo.jpg'),
         userInfo : {},
         topics : [],
         titles : []
      }
    },
    computed:{
    },
    methods : {
        getUserInfo () {
          const token = sessionStorage.getItem('token');
          if(token) {
            this.axios.get('/api/auth',{headers : {Authorization : 'Bearer ' + token}}).then((res) => {
                  console.log(res.data);
                  this.userInfo = res.data;
                  this.getArticles();
                  return this.axios.get('/api/getTopicTitles/' + this.userInfo.name,{headers : {Authorization : 'Bearer ' + token}})
                                    .then((res) => {
                                        console.log(res.data)
                                        this.titles = res.data;
                                    });
            }, (err) => {
                  console.log(err)
            })
          }
        },
        signOut () {
            console.log(12120)
            sessionStorage.clear();
            location.reload()
        },
        getArticles () {
            const token = sessionStorage.getItem('token');
            if(token) {
                this.axios.get('/api/get_topics/', {headers : {Authorization : 'Bearer ' + token}})
                .then((res) => {
                    console.log(res.data);
                    this.topics = res.data;
                }, (err) => {
                    console.log(err)
                })
            }
        },
        convertTime(postTime){
            let dpostTime = new Date(postTime);
            let mpostTime = moment(dpostTime);
            let now = moment();
            let dif = now.diff(mpostTime,'days');
            console.log(dif);
            return dif;
        },
        toggleArticle (route) {
            this.$router.go(route)
        }
    }
}
</script>

<style scoped>
.header {
  text-align:left;
  font-weight: 700;
  font-size: 1.28571429em;
  color: rgba(0,0,0,.87);
}
.layout-copy{
    text-align: center;
    padding: 10px 0 20px;
    color: #9ea7b4;
}
.img-position{
  padding-left : 12%;
}
.layout{
    /*border: 1px solid #d7dde4;
    background: #f5f7f9;*/
}
.layout-logo{
    width: 100px;
    height: 40px;
    border-radius: 3px;
    float: left;
    position: relative;
    top: 10px;
    left: 20px;
}
.layout-nav{
    /*display: flex;
    justify-content: flex-end;*/
}
ul{
   display: grid;
   grid-template-columns: 76% 24%;
}
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
    /*border-left: thin solid rgb(153,154,29);*/
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
</style>