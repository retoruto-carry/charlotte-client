<template>
  <form @submit.prevent>
    <div class="modal-card" style="width: auto">
      <header class="modal-card-head">
        <p class="modal-card-title">
          ユーザーを追加
        </p>
      </header>
      <section class="modal-card-body">
        <b-field label="ユーザー名">
          <b-input :value="name" placeholder="ユーザー名を入力" required />
        </b-field>
      </section>
      <footer class="modal-card-foot">
        <button class="button" type="button" @click="$parent.close()">
          キャンセル
        </button>
        <button class="button is-primary" @click="$emit('create')">
          追加する
        </button>
      </footer>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      default: ''
    }
  }
}
</script>

<style></style>
