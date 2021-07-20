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
            ...mapState(['pointbalance'])
        },
        methods:{
            async addFund(){
                const user = await Moralis.User.current();
                let addFunds = this.pointbalance + 1;
                user.set("balance",3)
                user.save()
            }
        },
        mounted(){
            this.addFund()
        }
    }
</script>

<style lang="scss" scoped>

</style>