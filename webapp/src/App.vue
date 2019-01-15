<template>
    <div>
        <Auth v-if="!isAuthenticated"></Auth>
        <div class="vh-100">
            <v-layout fill-height v-if="isAuthenticated">

                <Current :text="text"></Current>

            </v-layout>
        </div>
    </div>
</template>


<script>
    import Auth from './components/Auth';
    import Intro from './components/Intro.vue';
    import Current from './components/Current.vue';
    import {mapGetters} from 'vuex'

    export default {
        name: 'app',
        components: {Auth, Intro, Current},
        data() {
            return {
                active: null,
                text: ""
            }
        },
        methods: {},
        socket: {
            events: {
                change(msg) {
                    this.text = msg
                }
            }
        },
        created() {
            this.$store.dispatch('SESSION_CHECK')
        },
        computed:
            mapGetters([
                'isAuthenticated',
                'getUsername',
                'getUsername2',
                'getToken'
            ])
    }
</script>

<style>
    @import "./styles/main.css";
    @import '~vuetify/dist/vuetify.min.css';
    @import url('https://fonts.googleapis.com/css?family=Lato');

    @font-face {
        font-family: "IbmPlexSansThin";
        src: url("/static/font/ibmplexsans/IBMPlexSans-Thin.ttf") format("opentype");
    }

    @font-face {
        font-family: "IbmPlexSansRegular";
        src: url("/static/font/ibmplexsans/IBMPlexSans-Regular.ttf") format("opentype");
    }

    * {
        margin: 0px;
        padding: 0px;
        font-family: 'IbmPlexSansRegular', sans-serif;
    }

    .logo {
        font-family: 'IbmPlexSansThin', sans-serif !important;
    }


</style>
