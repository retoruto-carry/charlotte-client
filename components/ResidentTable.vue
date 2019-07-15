<template>
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
        <b-button
          size="is-small"
          type="is-danger"
          @click="$emit('deleteResident', props.row.id)"
        >
          ユーザー削除
        </b-button>
      </b-table-column>
    </template>
  </b-table>
</template>

<script>
export default {
  props: {
    residents: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style></style>
