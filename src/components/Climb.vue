<template>
    <div>
        <div class="open" @click="showClimb">Mostra <br> Scalata</div>
        <div v-show="show" class="climb flex">
            <div class="box-wrap" v-for="(item, index) in money" :key="index">
                <div class="box" :class="{green: (index <= (done.length - 2)), yellow: (index == (done.length - 1))}">{{item}}</div>
            </div>
            <div class="box-wrap">
                <div class="box" :class="{yellow: done.length == 15}">1 MILIONE</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Climb',
    props:{
        done: Array,
        money: Array,
    },
    data(){
        return {
            show: false,
        }
    },
    methods:{
        showClimb(){
            this.show = !this.show;
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/styles/variables.scss';

    .open{
        position: absolute;
        top: 5px;
        left: 5px;
        padding: 3px;
        background-color: $col-primary;
        border: 2px solid #fff;
        z-index: 10;
    }

    .climb{
        flex-direction: column-reverse;
        position: absolute;
        top: 20px;
        right: 20px;
        width: 400px;
        padding-bottom: 10px;
        
        .box{
            padding: 10px;
        }
        .green{
            background-color: #158a15;
        }
        .yellow{
            background-color: #e0a91b;
        }
    }

    // Media Query
    @media screen and (max-width:1600px){
        .climb{
            right: 0;
            width: 300px;
        }
    }
</style>