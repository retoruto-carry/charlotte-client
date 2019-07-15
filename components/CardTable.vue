<template>
  <b-table hoverable mobile-cards :data="cards">
    <template slot-scope="props">
      <b-table-column field="name" label="カード名" centered>
        {{ props.row.name }}
      </b-table-column>

      <b-table-column label="操作" centered>
        <b-button
          size="is-small"
          type="is-danger"
          @click="$emit('deleteCard', props.row.id)"
        >
          削除
        </b-button>
      </b-table-column>
    </template>
  </b-table>
</template>

<script>
export default {
  props: {
    cards: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style></style>
