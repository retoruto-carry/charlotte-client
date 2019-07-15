<template>
  <form @submit.prevent>
    <div class="modal-card" style="width: auto">
      <header class="modal-card-head">
        <p class="modal-card-title">
          ICカードを追加
          {{ lastUnknowTouchIdmDate }}
        </p>
      </header>
      <section class="modal-card-body">
        <b-field label="ICカード名">
          <b-input
            v-model="formData.name"
            placeholder="ICカード名を入力"
            required
          />
        </b-field>
      </section>
      <footer class="modal-card-foot">
        <button class="button" type="button" @click="$parent.close()">
          キャンセル
        </button>
        <button
          class="button is-primary"
          @click="$emit('createCard', formData)"
        >
          追加する
        </button>
      </footer>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: ''
      },
      lastUnknowTouchIdmDate: ''
    }
  },
  async created() {
    const { data } = await this.$axios.$get('last-unknown-touch-idm')
    this.lastUnknowTouchIdmDate = data.created_at
  }
}
</script>

<style></style>
