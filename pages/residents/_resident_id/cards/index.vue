<template>
  <section>
    <h1>{{ resident.name }}さんのカード一覧</h1>
    <b-button
      type="is-success"
      size="is-small"
      icon-left="plus"
      @click="isComponentModalActive = true"
    >
      カードを追加
    </b-button>
    <b-modal :active.sync="isComponentModalActive" has-modal-card>
      <card-create-modal-form @create="create()" />
    </b-modal>
    <h2 v-for="(card, index) in resident.cards" :key="index">
      {{ card.name }}
      <b-button type="is-danger" size="is-small" icon-left="delete">
        削除
      </b-button>
    </h2>
  </section>
</template>

<script>
import CardCreateModalForm from '~/components/CardCreateModalForm'
export default {
  components: {
    CardCreateModalForm
  },
  data() {
    return {
      resident: {
        name: null,
        cards: []
      },
      isComponentModalActive: false
    }
  },
  async created() {
    const { data } = await this.$axios.$get(
      `http://localhost/api/residents/${this.$route.params.resident_id}`
    )
    this.resident = data
  },
  methods: {
    create() {
      alert('create')
      this.isComponentModalActive = false
    }
  }
}
</script>

<style scoped>
h1 {
  font-size: 20px;
}
</style>
