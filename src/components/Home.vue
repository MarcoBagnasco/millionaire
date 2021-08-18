<template>
    <div class="home flex jc-center ai-center">
        <div v-if="begin" class="box-wrap begin">
            <div class="box" @click="playIntro">Inizia</div>
        </div> 

        <img v-else src="../assets/images/logo.png" alt="logo">

        <!-- Choose Mode -->
        <div v-if="mode" class="mode flex jc-center ai-center column">
            <div class="box-wrap">
                <div class="box">A che modalità vuoi giocare?</div>
            </div>
            <div class="flex jc-center ai-center wrap">
                <div class="box-wrap choice">
                    <div class="box" @click="$emit('playGame', true)">Scalata al Milione</div>
                </div>
                <div class="box-wrap choice">
                    <div class="box" @click="$emit('playGame', false)">Tutte le domande</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Home',
    data(){
        return{
            begin: true,
            mode: false,
        }
    },
    methods:{
        /**
         * Play intro and call choose
         */
        playIntro(){
            const intro = new Audio('/sounds/sigla.mp3');
            intro.play();
            this.begin = false;
            this.choose();
        },

        /**
         * Choose mode
         */
        choose(){
            setTimeout( () => {
                    this.mode = true;
                }
            ,3500)
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/styles/variables.scss';

    .home{
        padding: 40px;
        height: 100vh;
        background-color: $col-secondary;

        .begin{
            width: 500px;
            cursor: pointer;
        }

        img{
            max-height: 80%;
            max-width: 100%;
        }

        .mode{
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0, .7);

            .box-wrap{
                width: 600px;
            }

            .choice{
                margin: 10px;
                width: 300px;
                cursor: pointer;

                &:hover .box{
                    color: $col-primary;
                    background-color: #e0a91b;
                }
            }
        }
    }

    // Media Query
    @media screen and (max-width:639px){
        .home{
            .mode{
                .box-wrap{
                    width: 300px;
                }
            }
        }
    }
</style>