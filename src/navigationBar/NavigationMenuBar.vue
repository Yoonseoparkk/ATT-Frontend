<template>
    <v-app-bar color="orange" app dark height="64">
        <v-btn @click="goToHome">
            <v-toolbar-title class="text-uppercase text--darken-4">
                <span>ATT Project</span>
            </v-toolbar-title>
        </v-btn>
        <v-spacer></v-spacer>

        <v-btn text @click="goToBoardList" class="btn-text">
            <v-icon left>mdi-forum</v-icon>
            <span>게시판</span>
        </v-btn>
        <v-btn v-if="!isAuthenticated" text @click="signIn" class="btn-text">
            <v-icon left>mdi-login</v-icon>
            <span>로그인</span>
        </v-btn>
        <v-btn v-if="isAuthenticated" text @click="signOut" class="btn-text">
            <v-icon left>mdi-logout</v-icon>
            <span>로그아웃</span>
        </v-btn>
    </v-app-bar>
</template>

<script>
import '@mdi/font/css/materialdesignicons.css'
import router from '@/router'
import { mapActions, mapState } from 'vuex'

const naverAuthenticationModule = 'naverAuthenticationModule'

export default {
    data () {
        return {
        }
    },
    computed: {
        ...mapState(naverAuthenticationModule, ['isAuthenticated'])
    },
    methods: {
        ...mapActions(naverAuthenticationModule, ['requestLogoutToDjango']),
        goToHome () {
            router.push('/')
        },
        goToBoardList () {
            router.push('/board/list')
        },
        signIn () {
            router.push('/account/login')
        },
        signOut () {
            this.requestLogoutToDjango()
            router.push('/')
        },

    },
    mounted () {
        console.log('navigation bar mounted()')
        
        // const userToken = localStorage.getItem("userToken")

        // if (userToken) {
        //     console.log('You already have a userToken!!!')
        //     this.$store.state.authenticationModule.isAuthenticated = true
        // }
    },
}
</script>

<style scoped>
.status-indicator {
    margin-left: 5px;
    font-weight: bold;
    color: red;
}
</style>