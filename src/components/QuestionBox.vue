<template>
    <div class="QuestionBox">
        <div class="jumbotron">
            <h5>{{ question.question }}</h5>
            <hr class="my-4">
            <ul class="list-group">
                <li class="list-group-item"
                    v-for="(answer, index) in answers"
                    :key="index"
                    @click.prevent="selectAnswer(index)"
                    :class="[selectedIndex === index ? selected : '']"
                >
                    {{ answer }}
                </li>
            </ul>
            <button
                class="mx-2 btn btn-primary"
                @click="submitAnswer"
                :disabled="selectedIndex === null"
            >
            Submit
            </button>
            <button
                class="mx-2 btn btn-success"
                @click="next"
            >
            Next
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: "QuestionBox",
    props: {
        question: Object,
        next: Function,
        increment: Function
    },
    data() {
        return {
            selectedIndex: null,
            correctIndex: null,
            shuffledAnswers: [],
        }
    },
    computed: {
        answers() {
          let answers = [...this.question.incorrect_answers];
          answers.push(this.question.correct_answer);
          return answers;
        }
    },
    watch: {
        immediate: true,
        handler() {
            this.selectedIndex = null;
            this.shuffleAnswers();
        }
    },
    methods: {
        selectAnswer(index) {
            this.selectedIndex = index;
            console.log(this.selectedIndex);
        },
        shuffle(answerArr) {
            const preShuffledAnswers = [...answerArr];
            for (let i = preShuffledAnswers.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [preShuffledAnswers[i], preShuffledAnswers[j]] = [preShuffledAnswers[j], preShuffledAnswers[i]];
            }
            return preShuffledAnswers;
        },
        shuffleAnswers() {
            let answers = [...this.question.incorrect_answers, ...this.question.correct_answer];
            this.shuffledAnswers = this.shuffle(answers);
            this.correctIndex = this.shuffledAnswers.indexOf(this.question.correct_answer);
        },
        submitAnswer() {
            let isCorrect = false;
            if (this.selectedIndex === this.correctIndex) {
                isCorrect = true;
            }
            this.increment(isCorrect);
        }
    },
    mounted() {
        console.log('Hello world');
    }
}
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background: #EEE;
  cursor: pointer;
}
.btn {
  margin: 0 5px;
}
.selected {
  background-color: lightblue;
}
.correct {
  background-color: lightgreen;
}
.incorrect {
  background-color: red;
}
</style>
