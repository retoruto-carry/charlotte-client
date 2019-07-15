<template>
  <section>
    <b-button
      type="is-success"
      size="is-small"
      icon-left="plus"
      @click="isComponentModalActive = true"
    >
      住人を追加
    </b-button>

    <resident-table
      :residents="residents"
      @deleteResident="deleteResident($event)"
    />

    <b-modal :active.sync="isComponentModalActive" has-modal-card>
      <card-create-modal-form @createResident="createResident($event)" />
    </b-modal>
  </section>
</template>

<script>
import residentTable from '~/components/ResidentTable'
import CardCreateModalForm from '~/components/CardCreateModalForm'

export default {
  components: {
    residentTable,
    CardCreateModalForm
  },
  data() {
    return {
      residents: [],
      isComponentModalActive: false
    }
  },
  async created() {
    const { data } = await this.$axios.$get('http://localhost/api/residents/')
    this.residents = data
  },
  methods: {
    deleteResident(residentId) {
      alert(residentId)
    },
    createResident(form) {
      alert(form.name)
      this.isComponentModalActive = false
    }
  }
}
</script>
