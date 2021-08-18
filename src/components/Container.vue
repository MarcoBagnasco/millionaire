<template>
    <div class="main-content flex">
        <!-- Header -->
        <header class="main-header text-center">
            <img src="../assets/images/logo.png" alt="logo">
        </header>
        <!-- Game Area -->
        <div class="game-area">
            <!-- Questions -->
            <div v-if="!finish">
                <Question :quest="questions[num]"/>
                <Answers :climb="climb" :quest="questions[num]" @changeQuest="randQuest" @resp="add" @end="endGame"/>
                <Climb v-if="climb" :done="done" :money="money"/>
            </div>
            <!-- Results -->
            <div v-else class="text-center">
                <h1>Gioco Terminato!</h1>
                <h2>I tuoi risultati:</h2>
                <!-- Climb Results -->
                <div v-if="climb">
                    Hai vinto: € {{compute()}}
                </div>
                <!-- All Questions Results -->
                <div v-else class="flex jc-center ai-center wrap">
                    <div class="results">
                        <h3>Risposte esatte:</h3>
                        <div>{{exact}}</div>
                    </div>
                    <div class="results">
                        <h3>Risposte sbagliate:</h3>
                        <div>{{wrong}}</div>
                    </div>
                </div>
                <!-- Resume -->
                <div class="box-wrap">
                    <div class="box" @click="resume">Ricominica</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Question from './Question.vue';
import Answers from './Answers.vue';
import Climb from './Climb.vue';
import questions from '../questions.js';


export default {
    name: 'Container',
    components:{
        Question,
        Answers,
        Climb,
    },
    props:{
        climb: Boolean,
    },
    data(){
        return {
            finish: false,
            questions: questions,
            totQuest: questions.length,
            num: null,
            done: [],
            exact: 0,
            wrong: 0,
            money:['500', '1.000', '1.500', '2.000', '3.000', '5.000', '7.000', '10.000', '15.000', '20.000', '30.000', '70.000', '150.000', '300.000'],
            questClimb: 15,
        }
    },
    created(){
        this.randQuest();
    },
    methods:{
        /**
         * Show random Question
         */
        randQuest(){
            if((!this.climb && this.done.length != this.totQuest) || (this.climb && this.done.length != this.questClimb)){
                let randNum = Math.floor(Math.random() * this.totQuest);
                while(this.done.includes(randNum)){
                    randNum = Math.floor(Math.random() * this.totQuest);
                }
                this.num = randNum;
                this.done.push(randNum);
            } else {
                this.endGame();
            }
        },

        /**
         * Update Answers Lists
         */
        add(status){
            if(status){
                this.exact++;
            } else {
                this.wrong++;
            }
        },

        /**
         * End Game
         */
        endGame(){
            this.finish = true;
        },

        /**
         * Compute Gain
         */
        compute(){
            if(this.done.length === 0){
                return '0';
            } else if(this.done.length > 1 && this.exact < this.questClimb){
                return this.money[this.done.length - 2];
            } else {
                return '1 MILIONE!!!'
            }
        },

        /**
         * Resume Game
         */
        resume(){
            this.finish = false,
            this.done = [];
            this.exact = 0;
            this.wrong = 0;
            this.$emit('finish')
        },
    }
}
</script>

<style lang="scss" scoped>
@import '@/styles/variables.scss';

    .main-content{
        height: 100vh;
        flex-direction: column;
    }
    .main-header {
        padding: 40px;
        background-color: $col-secondary;

        img{
            max-width: 100%;
            max-height: 250px;
        }
    }

    .game-area{
        padding: 10px;
        flex-grow: 1;
        background-color: $col-primary;
    }

    .results{
        width: 250px;
        padding: 10px;
    }

    .box-wrap{
        width: 250px;
        margin: 20px auto;
        clip-path: $small;

        .box{
            clip-path: $small;
            cursor: pointer;
            &:hover{
                background-color: #158a15;
            }
        }
    }

    @media screen and (max-width:500px){
        .main-header {
            padding: 10px;

            img{
                max-width: 30%;
                max-height: 250px;
            }
        }      
    }
</style>