<template>
  <div class="container mt-2">
    <div v-for="(monitor, index) in monitors" :key="index">
      <b-card :title="monitor.subject" class="mb-2">
        <b-card-text>{{ monitor.description }}</b-card-text>

        <b-button variant="outline-secondary" class="mr-2" @click="edit(index)"> Editar </b-button>
        <b-button variant="outline-danger" class="mr-2" @click="remove(monitor, index)"> Excluir </b-button>
      </b-card>
    </div>

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
    }
  }
</script>