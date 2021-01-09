<template>
  <div>
    <b-card v-for="deck in decks" :key="deck.name">
      <b-row>
        <b-col>
          <nuxt-link
            :to="{ name: 'deck-id', params: { id: deck.id, name: deck.name } }"
            >{{ deck.name }}</nuxt-link
          >
        </b-col>
        <b-col>
          <b-row>Total {{ deck.total }}</b-row>
          <b-row>Due {{ deck.due }}</b-row>
          <b-row>New {{ deck.new }}</b-row>
          <b-row
            ><b-button size="sm" class="mb-2">
              <b-icon
                icon="trash"
                aria-hidden="true"
                v-on:click="deleteCard(deck.id)"
              ></b-icon> </b-button
          ></b-row>
          <b-row
            ><nuxt-link
            :to="{ name: 'card-create', params: { deck_id: deck.id} }"
            >
              <b-icon nuxt-link 
                icon="plus"
                aria-hidden="true"
              ></b-icon> </nuxt-link></b-row>
        </b-col>
      </b-row>
    </b-card>

    <deckCreateForm />
  </div>
</template>
<script>
import deckCreateForm from "../components/deckCreateForm.vue";
export default {
  components: { deckCreateForm },
  data: function() {
    return {
      decks: []
    };
  },
  mounted() {
    this.loadDecks();
  },
  methods: {
    loadDecks() {
      this.decks = this.$axios
        .get("http://127.0.0.1:8000/api/decks/")
        .then(response => (this.decks = response.data));
    },
    reload() {
      this.$forceUpdate();
    },
    async deleteCard(id) {
      await this.$axios({
        method: "DELETE",
        url: "http://127.0.0.1:8000/api/decks/delete",
        data: {
          deck_id: id
        }
      });
      this.loadDecks();
      this.reload();
    }
  }
};
</script>
