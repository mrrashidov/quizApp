<template>
  <div id="app">
    <div v-for="(question, index) in displayedQuestions" :key="index">
      <center>
        ID: {{ question.id }}<br />
        Question: {{ question.question }}

        <hr />
        <input
          type="text"
          v-model="answer"
          style="width: 50px; margin-right: 10px"
        />
        <button type="btn" @click="controlAnswer(question)">
          Check Answer
        </button>
      </center>
    </div>
  </div>
</template>


<script>
import items from "./answers.json";
export default {
  data() {
    return {
      questions: items,
      answer: "",
      page: 1,
      perPage: 1,
      pages: [],
    };
  },
  watch: {
    questions() {
      this.setPages();
    },
  },
  computed: {
    displayedQuestions() {
      return this.paginate(this.questions);
    },
  },
  methods: {
    controlAnswer(question) {
      if (question.answer === this.answer) {
        this.answer = "";
        return (this.page = this.page + 1);
      }
      return alert("Wrong Answer");
    },
    setPages() {
      var numberOfPages = Math.ceil(this.questions.length / this.perPage);
      for (var index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate(questions) {
      var page = this.page;
      var perPage = this.perPage;
      var from = page * perPage - perPage;
      var to = page * perPage;
      return questions.slice(from, to);
    },
  },
};
</script>