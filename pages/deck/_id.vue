<template>
  <div v-if="this.requestIndex < this.cards.length">
    <div v-if="loaded" class="container">
      <div>
        {{ cards[this.requestIndex].question }}
        <div v-if="showAnswerActive">
          {{ cards[this.requestIndex].answer }}
        </div>
      </div>

      <b-button v-if="!showAnswerActive" @click="showAnswer" variant="primary"
        >Show answer</b-button
      >
      <div v-if="showAnswerActive">
        <b-button @click="selectAnswerLevel(0,cards[requestIndex].id)" variant="primary"
          >Снова</b-button
        >
        <b-button @click="selectAnswerLevel(3,cards[requestIndex].id)" variant="primary"
          >Плохо</b-button
        >
        <b-button @click="selectAnswerLevel(4,cards[requestIndex].id)" variant="primary"
          >Хорошо</b-button
        >
        <b-button @click="selectAnswerLevel(5,cards[requestIndex].id)" variant="primary"
          >Отлично</b-button
        >
      </div>
    </div>
  </div>
  <div v-else>
    Нет карточек для повторения
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      loaded: false,
      showAnswerActive: false,
      cards: [],
      requestIndex: 0
    };
  },
  async created() {
    await this.$axios
      .get("http://127.0.0.1:8000/api/deck/", {
        params: {
          deck_id: this.$route.params.id
        }
      })
      .then(response => (this.cards = response.data));
    this.loaded = true;
  },
  methods: {
    showAnswer() {
      this.showAnswerActive = true;
    },
    selectAnswerLevel(answer_quality,card_id) {
      this.requestIndex++;
      this.showAnswerActive = false;
      this.$axios.post("http://127.0.0.1:8000/api/card/changedate", {
        card_id: card_id,
        answer_quality: answer_quality
      });
    }
  }
};
</script>
