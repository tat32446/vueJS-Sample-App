<template>
  <div class="question-box-container">
    <b-jumbotron>
      <template v-slot:lead>{{currentquestion.question}}</template>

      <hr class="my-4" />

      <b-list-group >
        <b-list-group-item v-for="(answer,index) in answers" 
       :key="index" 
       @click="selectAnswer(index)"
       :class="[selectedIndex === index ? 'selected' : '']"
        
        
        >{{answer}}</b-list-group-item>
      </b-list-group>

      <b-button variant="primary" href="#">Submit</b-button>
      <b-button @click="next" variant="success" href="#">Next</b-button>
    </b-jumbotron>
  </div>
</template>
<script>
export default {
  props: {
    currentquestion: Object,
    next: Function
  },
  data(){
    return {
      selectedIndex:null

    }
  },
  computed: {
    answers() {
      let answers = [...this.currentquestion.incorrect_answers];
      answers.push(this.currentquestion.correct_answer);
      return answers;
    }
  },
  watch:{
    currentQuestion(){
      this.selectedIndex=null
      this.suuffleAnswers()
    }

  },
  methods:{
    selectAnswer(index){
      this.selectedIndex=index
     },
    suuffleAnswers(){
       let answers = [...this.currentquestion.incorrect_answers,this.currentQuestion.correct_answer];

    }

 

  }
};
</script>

<style scoped>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background: #EEE;
  cursor: pointer
}
.btn {
  margin: 0 5px;
}
.selected{
  background-color:lightblue
}
.correct{
  background-color: lightgreen
}
.incorrect{
  background-color:red
  }
</style>