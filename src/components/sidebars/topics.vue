<template>
<div class="layout-content-main">
    <Card>
        <div class="topics">
            <div class="header">你的话题</div>
            <div class="divider"></div>
            <div class="linklists" id="user_card_list">
                <template v-for="title in this.$props.titles">
                    <router-link :to="{name: 'article', params: { user:profile.name, uid:title._id}}" class="item">
                        {{title.title}}
                    </router-link>
                </template>
                <!--<a class="item" href="/topic/2">Tests</a>
                <a class="item" href="/topic/1">Computed Properties and Watchers</a>-->
            </div>
        </div>
        <template v-if="Object.keys(profile).length > 0">
        <router-link :to="{name: 'peditor', params: { userid: profile.name}}" class="create-topic">
            <div class="visible">
                <Icon type="plus-round"></Icon>
                发表话题
            </div>
        </router-link>
        </template>
    </Card>
</div>
</template>

<script>

export default {
    props: {
        profile: {
            type: Object,
            default: {}
        },
        titles: {
            tyep: Array,
            default: () => []
        }
    },
    watch:{
      '$route':'fetchData'
    },
    components : {
        
    },
    created(){
    },
    data () {
      return {
      }
    },
    methods : {
        fetchData() {
            //this.$router.push(this.$route.path)
            this.$emit('article', this.$route.path)
            //console.log(this.$route.path)
            console.log(12121212)
        }
    }
}
</script>

<style scoped>
.divider {
    border-top: 1px solid rgba(34,36,38,.15);
    margin: 1rem 0;
}
.header {
    text-align:left;
    font-weight: 700;
    font-size: 1.28571429em;
    color: rgba(0,0,0,.87);
}
.item {
    color: rgba(0,0,0,.4);
    text-align: left;
}  
.linklists {
    display: flex;
    flex-direction: column;
}

a.create-topic {
    color: #a812e8;
}

.visible {
    padding: 3px;
    border: 1px solid;
    transition: all 0.3s ease 0s;
}

div.visible:hover {
    background: #d5abe8;
}

a.item:hover {
    color: #d5abe8;
}
</style>