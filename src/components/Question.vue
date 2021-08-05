<template>
    <div class="container">
        <div class="question flex jc-center">
            <div class="box-quest box-wrap">
                <div class="box">{{quest.question}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Question',
    props:{
        quest: Object,
    },
}
</script>

<style lang="scss" scoped>
@import '@/styles/variables.scss';

    .question{
        margin: 20px 0;
        .box-quest{
            width: 750px;
        }
    }


    // Media Queries
    @media screen and (max-width:900px){
        .box-quest{
            width: 450px;
            clip-path: $big;

            .box{
                clip-path: $big;
            }
        }
    }
    @media screen and (max-width:500px){
        .box-quest{
            width: 300px;
            clip-path: $medium;

            .box{
            clip-path: $medium;
            }
        }
    }
</style>