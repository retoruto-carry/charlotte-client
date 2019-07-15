<template>
  <section>
    <b-table hoverable mobile-cards :data="residents">
      <template slot-scope="props">
        <b-table-column field="name" label="ユーザー名" centered>
          {{ props.row.name }}
        </b-table-column>

        <b-table-column label="操作" centered>
          <b-button
            size="is-small"
            type="is-primary"
            tag="router-link"
            :to="`residents/${props.row.id}/cards`"
          >
            カード詳細
          </b-button>
          <b-button size="is-small" type="is-danger">
            ユーザー削除
          </b-button>
        </b-table-column>
      </template>
    </b-table>
  </section>
</template>

<script>
export default {
  data() {
    return {
      residents: []
    }
  },
  async created() {
    const { data } = await this.$axios.$get('http://localhost/api/residents/')
    this.residents = data
  }
}
</script>
