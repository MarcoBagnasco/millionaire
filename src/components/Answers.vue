<template>
    <div class="container">
        <div class="flex jc-center wrap">
            <div v-for="(item, index) in quest.answers" :key="index" class="box-ans box-wrap">
                <div class="box" :class="{choice: active,correct : correct && current == item, uncorrect : uncorrect && current == item}" @click="response(item)">{{letters[index] + ': ' + item}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Answers',
    props:{
        quest: Object,
    },
    data(){
        return {
            letters: ['A', 'B', 'C', 'D'],
            active: true,
            current: '',
            correct: false,
            uncorrect: false,
            correctSound: new Audio('/sounds/correct.mp3'),
            uncorrectSound: new Audio('/sounds/uncorrect.mp3'),
        }
    },
    methods:{
        /**
         * Envaluate response
         */
        response(item){
            if(this.active){
                this.active = false;
                this.current = item;
                if(item === this.quest.rightAnswer){    
                    this.correctSound.play();
                    this.correct = true;
                    this.$emit('resp', true);
                } else {    
                    this.uncorrectSound.play();
                    this.uncorrect = true;
                    this.$emit('resp', false);
                }
                setTimeout(this.next,2500)
            }
        },
        /**
         * Next Question
         */
        next(){
            this.active = true;
            this.current = '';
            this.correct = false;
            this.uncorrect = false;
            this.$emit('change');
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/styles/variables.scss';

    .box-ans{
        width: calc(50% - 40px);
        margin: 10px 20px;
        clip-path: $medium;

        .box{
            clip-path: $medium;

            &.correct{
                animation: correct linear .6s 3 forwards;
            }
            &.uncorrect{
                background-color: #b50000;
            }
        }
        .choice:hover{
            color: $col-primary;
            background-color: #e0a91b;
            cursor: pointer;
        }
    }

    // Animation
    @keyframes correct {
        from, 50%{
            background-color: $col-primary;
        }
        51%, to{
            background-color: #158a15;
        }
    }

    // Media Queries
    @media screen and (max-width:900px){
        .box-ans{
            width: 250px;
            clip-path: $small;

            .box{
            clip-path: $small;
            }
        }

        .box-ans{
            .choice:hover{
                color: #fff;
                background-color: $col-primary;
            }
        }
    }
</style>