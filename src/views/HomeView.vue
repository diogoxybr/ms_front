<template>
  <div class="container mt-2">
    <template v-if="isMonitorsEmpty">
      <div class="empty-data mt-5">
        <img src="../assets/images/emptygarden.svg" class="empty-data-image">
        <b-button
        variant="outline-primary"
        class="mt-5"
        size="lg"
        to="form"
        > Clique aqui para fazer seu primeiro plantio ! </b-button>
      </div>
    </template>
    <template v-else>
    <div v-for="(monitor, index) in monitors" :key="index">
      <b-card :title="monitor.subject" class="mb-2">
        <b-card-text>{{ monitor.description }}</b-card-text>

        <b-button variant="outline-secondary" class="mr-2" @click="edit(index)"> Editar </b-button>
        <b-button variant="outline-danger" class="mr-2" @click="remove(monitor, index)"> Excluir </b-button>
      </b-card>
    </div>
    </template>
    <template v-if="!isMonitorsEmpty">
        <b-button
        variant="outline-primary"
        to="form"
        > Cadastrar novo plantio </b-button>
    </template>
    <b-modal ref="modalRemove" hide-footer title="Exclusão de monitoramento">
      <div class="dblock text-center">
        Deseja realmente excluir o monitoramento {{ monitorSelected.subject }} ?
      </div>
      <div class="mt-3 d-flex justify-content-end">
        <b-button variant="outline-secondary" class="mr-2" @click="hideModal"> Cancelar </b-button>
        <b-button variant="outline-danger" class="mr-2" @click="confirmRemoveMonitor"> Confirmar </b-button>
      </div>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "HomeView",

  data() {
    return{
      monitors: [],
      monitorSelected: []
      }
    },

    created() {
      this.monitors = (localStorage.getItem("monitors")) ? JSON.parse(localStorage.getItem("monitors")) : [];

    },

    methods: {
      edit(index) {
        this.$router.push({ name:"form", params: { index } });
      },
      remove(monitor, index) {
        this.monitorSelected = monitor;
        this.monitorSelected.index = index;
        this.$refs.modalRemove.show();
      },

      hideModal() {
        this.$refs.modalRemove.hide();
      },

      confirmRemoveMonitor() {
        this.monitors.splice(this.monitorSelected.index, 1);
        localStorage.setItem("monitors", JSON.stringify(this.monitors));
        this.hideModal();
      }
    },

    computed: {
      isMonitorsEmpty() {
        return this.monitors.length === 0;
      }
    }
  }
</script>

<style scoped>
.empty-data {
  display: flex;
  align-items: center;
  flex-direction: column;
}
.empty-data-image {
  width: 500px;
}
</style>