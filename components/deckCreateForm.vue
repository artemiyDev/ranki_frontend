<template>
  <div>
    <b-button v-b-toggle.collapse-1 v-on:click= "show=true" variant="primary"
      >Создать новую колоду</b-button
    >
    <b-collapse id="collapse-1" class="mt-2"  v-if="show">
      <b-form @submit="onSubmit">
        <b-form-group id="input-group-name">
          <b-form-input
            id="input-2"
            v-model="form.name"
            placeholder="Введите название"
            required
          ></b-form-input>
        </b-form-group>
        <b-button type="submit" variant="primary">Создать</b-button>
      </b-form>
    </b-collapse>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: ""
      },
      show: true
    };
  },
  methods: {
    onSubmit(event) {
      event.preventDefault();
      this.$axios.post(
        "http://127.0.0.1:8000/api/decks/create",
        JSON.stringify(this.form),
        { headers: { "Content-Type": "application/json" } }
      );
      this.show = false;
      this.$parent.loadDecks()
      this.$parent.reload()
    }
  }
};
</script>
