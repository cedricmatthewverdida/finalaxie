<template>
    <div>
        HAHAHAHAHAHA
    </div>
</template>

<script>
    const Moralis = require("moralis")
    import { mapState } from 'vuex'
    export default {
        computed:{
            ...mapState(['user'])
        },
        mounted(){
            // const currentUser =  Moralis.User.current();
            // let addFunds = this.pointbalance + 1;
            // currentUser.set("balance",1)
            // currentUser.save()
            console.log(this.user);
        }
    }
</script>

<style lang="scss" scoped>

</style>