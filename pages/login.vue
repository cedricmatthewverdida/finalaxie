<template>
    <div style="margin-top:150px">
        <div  class="d-flex justify-center">
            <v-sheet width="100px" color="transparent">
            
            <v-img
                :src="require('@/assets/metamask.png')"
                :lazy-src="require('@/assets/metamask.png')"
                >
            </v-img>
            </v-sheet>
        </div>

        <div class="d-flex justify-center text-center">
            <v-sheet width="400px" color="transparent">
            
            <h1>Welcome Player</h1>

            <small >Please connect Metamask to get started</small>
            
            

            <v-container>
                <v-btn
                class="mt-2"
                x-large
                rounded
                block
                color="primary"
                :loading="authorize"
                @click="loginMetamask()"
                
                >
                <v-icon>mdi-ethereum</v-icon>
                Connect metamask</v-btn>
            </v-container>
            </v-sheet>
        </div>
    </div>
</template>

<script>
    import { mapState,mapActions } from 'vuex'
    import Moralis from 'moralis';
    export default {

        middleware: 'is_loggedin',
        data: () => ({
        authorize: false,
        message: ''
        }),
        methods:{
            ...mapActions(['loggedin']),
            async loginMetamask (){
                if(window.ethereum){

                    this.authorize = true;
                    try{

                        let user = await Moralis.Web3.authenticate();
                   
                        if(user){
                            this.set_User(user);
                            this.authorize = false;
                            this.loggedin();
                            this.$router.push('/')
                        }

                    }catch{
                        this.authorize = false;
                    }
                }else{
                    this.message = "Please install MetaMask first";
                }
            },

            set_User (token){
            this.$store.commit('authorize_loggin', token)
            },

        },
        computed:{
            ...mapState(['user'])
        },
        
    }
</script>

<style>

.glass_effect{
    backdrop-filter: blur(0px) saturate(180%);
    -webkit-backdrop-filter: blur(0px) saturate(180%);
    background-color: rgba(17, 25, 40, 0.75);
    border-radius: 12px;
    border: 1px solid rgba(255, 255, 255, 0.125);
}

</style>