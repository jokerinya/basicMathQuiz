<template>
  <div class="panel panel-default">
    <div class="panel-heading">
      <h3 class="panel-title text-center">{{ question }}</h3>
    </div>
    <div class="panel-body">
      <div class="col-xs-12 col-sm-6 text-center">
        <!-- true olarak butonlardan bir tanesinden bilgi dönecek. -->
        <button
          class="btn btn-primary btn-lg"
          style="margin: 10px"
          @click="answerIs(btn[0].correct)"
        >{{btn[0].answer}}</button>
      </div>
      <div class="col-xs-12 col-sm-6 text-center">
        <button
          class="btn btn-primary btn-lg"
          style="margin: 10px"
          @click="answerIs(btn[1].correct)"
        >{{btn[1].answer}}</button>
      </div>
      <div class="col-xs-12 col-sm-6 text-center">
        <button
          class="btn btn-primary btn-lg"
          style="margin: 10px"
          @click="answerIs(btn[2].correct)"
        >{{btn[2].answer}}</button>
      </div>
      <div class="col-xs-12 col-sm-6 text-center">
        <button
          class="btn btn-primary btn-lg"
          style="margin: 10px"
          @click="answerIs(btn[3].correct)"
        >{{btn[3].answer}}</button>
      </div>
    </div>
  </div>
</template>
<style>
</style>
<script>
export default {
  data() {
    return {
      question: 0,
      situation: 1,
      correctAnswer: 0,
      btn: [
        { correct: false, answer: 1 },
        { correct: false, answer: 2 },
        { correct: false, answer: 3 },
        { correct: true, answer: 4 }
      ]
    };
  },
  methods: {
    generateQuestion() {
      this.situation = this.generateNumber(1, 2); //topla çıkart 1-2
      let from = this.generateNumber(1, 100);
      let to = this.generateNumber(1, 100);
      if (this.situation == 1) {
        this.question = "What is " + from + "+" + to + "= ?";
        this.correctAnswer = from + to;
      } else {
        this.question = from + "-" + to + "= ?";
        this.correctAnswer = from - to;
      } //topla çıkart bitti doğru cevap belirlendi

      this.btn[0].correct = false;
      this.btn[0].answer = this.generateNumber(
        this.correctAnswer - 10,
        this.correctAnswer + 10,
        this.correctAnswer
      );
      this.btn[1].correct = false;
      this.btn[1].answer = this.generateNumber(
        this.correctAnswer - 10,
        this.correctAnswer + 10,
        this.correctAnswer
      );
      this.btn[2].correct = false;
      this.btn[2].answer = this.generateNumber(
        this.correctAnswer - 10,
        this.correctAnswer + 10,
        this.correctAnswer
      );
      this.btn[3].correct = false;
      this.btn[3].answer = this.generateNumber(
        this.correctAnswer - 10,
        this.correctAnswer + 10,
        this.correctAnswer
      ); // tüm şıklara bir değer atandı ve hepsi false yapıldı

      let correctSelect = this.generateNumber(0, 3);
      this.btn[correctSelect].correct = true;
      this.btn[correctSelect].answer = this.correctAnswer;
      //rastgele bir şık seçildi ve doğru olarak atandı
    },
    generateNumber(min, max, except) {
      let num = Math.floor(Math.random() * (max - min + 1)) + min;
      if (except == num) {
        return (num = Math.floor(Math.random() * (max - min + 1)) + min);
      }
      return num;
    },
    answerIs(answer) {
      //app e haber vermeli
      if (answer) {
        this.$emit("answerTrue", answer);
      } else {
        alert("Wrong, Try Again");
      }
    }
  },
  created() {
    this.generateQuestion();
  }
};
</script>
