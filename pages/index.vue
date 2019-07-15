<template>
  <section>
    <b-button
      type="is-success"
      size="is-small"
      icon-left="plus"
      @click="isCardCreateFormModalActive = true"
    >
      住人を追加
    </b-button>

    <resident-table
      :residents="residents"
      @deleteResident="deleteResident($event)"
    />

    <b-modal :active.sync="isCardCreateFormModalActive" has-modal-card>
      <card-create-form-modal @createResident="createResident($event)" />
    </b-modal>
  </section>
</template>

<script>
import residentTable from '~/components/ResidentTable'
import CardCreateFormModal from '~/components/CardCreateFormModal'

export default {
  components: {
    residentTable,
    CardCreateFormModal
  },
  data() {
    return {
      residents: [],
      isCardCreateFormModalActive: false
    }
  },
  async created() {
    const { data } = await this.$axios.$get('residents')
    this.residents = data
  },
  methods: {
    deleteResident(residentId) {
      alert(residentId)
    },
    createResident(form) {
      alert(form.name)
      this.isCardCreateFormModalActive = false
    }
  }
}
</script>
