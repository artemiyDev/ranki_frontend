<template>
  <div>
    <b-form @submit="onSubmit">
      <b-form-group id="input-group-1" label="Вопрос:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="question"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Ответ:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="answer"
          required
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary">Создать</b-button>
      <b-button  v-on:click="cancelCardCreation" variant="danger">Отмена</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
        question: "",
        answer: ""
    }
  },
  methods: {
    onSubmit(event) {
      event.preventDefault()
      this.$axios.post(
        "http://127.0.0.1:8000/api/card/create",
        {
          question:this.question,
          answer:this.answer,
          deck_id:this.$route.params.deck_id
        }
      )
      this.$router.push("/decks");
    },
    cancelCardCreation() {
      this.$router.push("/decks");
    }
  }
};
</script>
