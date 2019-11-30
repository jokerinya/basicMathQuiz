<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1 class="text-center">The Super Quiz</h1>
      </div>
    </div>
    <hr />
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <transition name="switch" mode="out-in">
          <component :is="mode" @answerTrue="mode='app-answer'" @confirm="mode='app-question'"></component>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import Question from "./components/Question.vue";
import Answer from "./components/Answer.vue";

export default {
  data() {
    return {
      mode: "app-question"
    };
  },
  components: {
    appAnswer: Answer,
    appQuestion: Question
  }
};
</script>

<style>
.switch-enter-active {
  animation: starter 0.5s ease-in-out;
}

.switch-leave-active {
  animation: follower 0.5s ease-in-out;
}

@keyframes starter {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}

@keyframes follower {
  from {
    transform: rotateY(0deg);
  }
  to {
    transform: rotateY(90deg);
  }
}
</style>

