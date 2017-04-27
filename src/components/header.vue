<template>
    <div class="header">
        <div class="container">
            <div class="logo"><router-link to="/"><img src="/static/img/logo.png" alt="眼镜日记" width="150" height="50"></router-link></div>
            <div class="nav clearfix">
                <ul>
                    <li><router-link to="/"  class="nav_a" active-class="nav_active" exact>主页</router-link></li>
                    <li><router-link to="/dairy" class="nav_a" active-class="nav_active">日记</router-link></li>
                    <li><router-link to="/photo" class="nav_a" active-class="nav_active">照片墙</router-link></li>
                    <li v-if="!getAuth"><router-link to="/login" class="nav_a" active-class="nav_active">登录</router-link></li>
                    <li v-else>
                        <a href="javascript:void(0)" class="nav_user">
                            <img :src="getAuth.header" class="circle" width="30" height="30"> {{getAuth.nickname}}
                            <ul class="nav_user_ul">
                                <li><router-link :to="{ name: 'userIndex', params: { uid: getAuth.id }}">我的主页</router-link></li>
                                <li><router-link :to="{ name: 'userAlbum', params: { uid: getAuth.id }}">我的相册</router-link></li>
                                <li><router-link to="/set/">管理中心</router-link></li>
                                <li class="nav_user_line"></li>
                                <li><a href="javascript:void(0)" class="text-center" @click="logout()">退出</a></li>
                            </ul>
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    import { mapGetters ,mapActions } from 'vuex'

    export default {
        data(){
            return {

            }
        },
        computed: {
            ...mapGetters({
                getToken: 'getToken',
                getAuth:'getAuth'
            }),
            ...mapActions({
                userLogout: 'userLogout',
                authInfo: 'authInfo'
            })
        },
        mounted(){
            if(this.getToken){
                this.$store.dispatch('authInfo');
            }
        },
        methods:{
            logout(){
                this.$store.dispatch('userLogout');
            }
        }
    }
</script>
