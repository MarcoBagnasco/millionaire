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
                <Answers :quest="questions[num]" @change="randQuest" @resp="add"/>
            </div>
            <!-- Results -->
            <div v-else class="text-center">
                <h1>Gioco Terminato!</h1>
                <h2>I tuoi risultati:</h2>
                <div class="flex jc-center ai-center wrap">
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
import questions from '../questions.js';


export default {
    name: 'Container',
    components:{
        Question,
        Answers,
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
            if(this.done.length != this.questions.length){
                let randNum = Math.floor(Math.random() * this.totQuest);
                while(this.done.includes(randNum)){
                    randNum = Math.floor(Math.random() * this.totQuest);
                }
                this.num = randNum;
                this.done.push(randNum);
            } else {
                this.finish = true;
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