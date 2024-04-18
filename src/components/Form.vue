<template>
    <div v-if="isSubmit" id="result">
        <Result :marks="marks" :total="questions.length" :attempted="attemptCount"  @reset-all="resetAll" />
    </div>
    <div v-else id="main">
        <h1 class="title">Online Quiz </h1>
        <Track :questions="questions" :currentQuestion="currentQuestion" @change-question="changeQuestion" />

        <fieldset>
            <legend>Question-{{ currentQuestion + 1 }}</legend>
            <section>
                <div class="form">
                    <label for="">{{ questions[currentQuestion].question }}</label>
                    <ol>
                        <li v-for="(opt, index) in questions[currentQuestion].options" @click="selection(index)">
                            <span
                                :class="questions[currentQuestion].selected !== null ? (index === questions[currentQuestion].answer ? 'rightAns' : 'wrongAns') : ''">
                                {{ opt }}
                            </span>
                            <span v-show="index == questions[currentQuestion].selected">
                                <span v-if="questions[currentQuestion].result == true">✔️</span>
                                <span v-else>❌</span>
                            </span>
                        </li>
                    </ol>
                </div>
                <div class="buttons">
                    <button v-if="currentQuestion != 0" @click="previousQuestion">Previous</button>
                    <button v-if="currentQuestion != questions.length - 1" @click="nextQuestion">Next</button>
                    <button v-if="attemptCount > 0" @click="submitQuiz">Submit</button>
                </div>
            </section>
        </fieldset>
        <Instruction />
    </div>
</template>
<script>
import Result from './Result.vue';
import Track from './Track.vue';
import Instruction from './Instruction.vue';
export default {
    name: "Form",
    components: {
        Result,
        Track,
        Instruction
    },

    data() {
        return {
            currentQuestion: 0,
            attemptCount: 0,
            marks: 0,
            isSubmit: false,
            questions: [
                {
                    "question": "What is the full form of HTML?",
                    "options": [
                        "Hyper Text Markup Language",
                        "Highly Technical Modern Language",
                        "Hypertext Transfer Markup Language",
                        "Home Tool Management Language"
                    ],
                    "answer": 0,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "What does CPU stand for?",
                    "options": [
                        "Central Processing Unit",
                        "Computer Peripheral Unit",
                        "Central Peripheral Unit",
                        "Computer Processing Unit"
                    ],
                    "answer": 0,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "Which programming language is known for its readability and simplicity?",
                    "options": [
                        "Java",
                        "C++",
                        "Python",
                        "Ruby"
                    ],
                    "answer": 2,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "What is the chemical symbol for water?",
                    "options": [
                        "H2O",
                        "CO2",
                        "O2",
                        "CH4"
                    ],
                    "answer": 0,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "Which planet is known as the “Red Planet”?",
                    "options": [
                        "Earth",
                        "Mars",
                        "Venus",
                        "Jupiter"
                    ],
                    "answer": 1,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "Who wrote the play “Romeo and Juliet”?",
                    "options": [
                        "Charles Dickens",
                        "William Shakespeare",
                        "Jane Austen",
                        "Mark Twain"
                    ],
                    "answer": 1,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "What is the capital city of Japan?",
                    "options": [
                        "Beijing",
                        "Seoul",
                        "Tokyo",
                        "Bangkok"
                    ],
                    "answer": 2,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "Which gas do plants absorb during photosynthesis?",
                    "options": [
                        "Oxygen",
                        "Nitrogen",
                        "Carbon dioxide",
                        "Hydrogen"
                    ],
                    "answer": 2,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "What is the largest mammal on Earth?",
                    "options": [
                        "African elephant",
                        "Blue whale",
                        "Giraffe",
                        "Polar bear"
                    ],
                    "answer": 1,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                },
                {
                    "question": "Who painted the famous artwork “Mona Lisa”?",
                    "options": [
                        "Vincent van Gogh",
                        "Pablo Picasso",
                        "Leonardo da Vinci",
                        "Michelangelo"
                    ],
                    "answer": 2,
                    "selected": null,
                    "isAttempted": false,
                    "result": false
                }
            ]
        }
    },

    created() {
        window.onbeforeunload = function () {
            return "handle your events or msgs here";
        }
    },
    
    methods: {
        nextQuestion() {
            this.currentQuestion++
        },
        previousQuestion() {
            this.currentQuestion--
        },
        changeQuestion(i) {
            this.currentQuestion = i
        },
        selection(i) {
            if (this.questions[this.currentQuestion].selected == null) {
                this.questions[this.currentQuestion].isAttempted = true;
                this.attemptCount++;
                this.questions[this.currentQuestion].selected = i;
                if (this.questions[this.currentQuestion].selected == this.questions[this.currentQuestion].answer) {
                    this.questions[this.currentQuestion].result = true;
                }
            }

        },

        submitQuiz() {
            console.log(this.attemptCount );
            if (this.attemptCount < 10) {
                if (window.confirm("Would you want to submit the quiz?")) {
                    this.questions.map(q => q.result && this.marks++)
                    this.isSubmit = true;
                }
            }else{
                this.questions.map(q => q.result && this.marks++)
                    this.isSubmit = true;
            }
        },

        resetAll() {
            this.currentQuestion = 0,
                this.marks = 0,
                this.isSubmit = false,
                this.questions = [
                    {
                        "question": "What is the full form of HTML?",
                        "options": [
                            "Hyper Text Markup Language",
                            "Highly Technical Modern Language",
                            "Hypertext Transfer Markup Language",
                            "Home Tool Management Language"
                        ],
                        "answer": 0,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "What does CPU stand for?",
                        "options": [
                            "Central Processing Unit",
                            "Computer Peripheral Unit",
                            "Central Peripheral Unit",
                            "Computer Processing Unit"
                        ],
                        "answer": 0,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "Which programming language is known for its readability and simplicity?",
                        "options": [
                            "Java",
                            "C++",
                            "Python",
                            "Ruby"
                        ],
                        "answer": 2,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "What is the chemical symbol for water?",
                        "options": [
                            "H2O",
                            "CO2",
                            "O2",
                            "CH4"
                        ],
                        "answer": 0,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "Which planet is known as the “Red Planet”?",
                        "options": [
                            "Earth",
                            "Mars",
                            "Venus",
                            "Jupiter"
                        ],
                        "answer": 1,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "Who wrote the play “Romeo and Juliet”?",
                        "options": [
                            "Charles Dickens",
                            "William Shakespeare",
                            "Jane Austen",
                            "Mark Twain"
                        ],
                        "answer": 1,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "What is the capital city of Japan?",
                        "options": [
                            "Beijing",
                            "Seoul",
                            "Tokyo",
                            "Bangkok"
                        ],
                        "answer": 2,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "Which gas do plants absorb during photosynthesis?",
                        "options": [
                            "Oxygen",
                            "Nitrogen",
                            "Carbon dioxide",
                            "Hydrogen"
                        ],
                        "answer": 2,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "What is the largest mammal on Earth?",
                        "options": [
                            "African elephant",
                            "Blue whale",
                            "Giraffe",
                            "Polar bear"
                        ],
                        "answer": 1,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    },
                    {
                        "question": "Who painted the famous artwork “Mona Lisa”?",
                        "options": [
                            "Vincent van Gogh",
                            "Pablo Picasso",
                            "Leonardo da Vinci",
                            "Michelangelo"
                        ],
                        "answer": 2,
                        "selected": null,
                        "isAttempted": false,
                        "result": false
                    }
                ]
        },

    }
}
</script>
<style scoped>
*::selection {
    user-select: none;
}

#main {
    height: 700px;
    width: 900px;
    background: white;
    color: gray;
    border-radius: 10px;
}


.title {
    width: 100%;
    padding: 20px 0px;
    text-align: center;
}

fieldset {
    height: 60%;
    width: 80%;
    margin: auto;
    border-radius: 10px;
    padding: 25px;

}

legend {
    font-weight: bold;
    margin: 0 20px;
    padding: 0 5px;
}

section {
    height: 100%;
    width: 100%;
}

.form {
    height: 90%;
    width: 100%;
}

.form>label {
    font-weight: 500;
    font-size: x-large;
}

.form>ol {
    padding: 15px 20px;
    list-style: lower-alpha;
}

ol>li:hover {
    background: #dfdcdc;
    border-radius: 5px;
    cursor: pointer;
}

.rightAns {
    color: green;
}

.wrongAns {
    color: red;
}

ol>li {
    padding: 10px;
}

.buttons {
    height: 10%;
    margin: 10px 0px;
    display: flex;
    justify-content: end;
    align-items: center;
    width: 100%;
    column-gap: 5px;
}

.buttons>button {
    width: 10%;
    padding: 5px 0px;
    font-weight: bold;
    background-color: antiquewhite;
    border: 1px solid;
    border-radius: 5px;
    cursor: pointer;
}

.buttons>button:hover {
    background-color: rgb(229, 197, 155);
}
</style>