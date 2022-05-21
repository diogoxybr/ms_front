<template>
  <div class="container mt-2">
    <b-form>
      <b-form-group
        label= "Titulo"
        label-for="subject"
      >
        <b-form-input
          id="subject"
          v-model.trim="$v.form.subject.$model"
          type="text"
          placeholder="Ex: alface"
          required
          autocomplete="off"
          :state="getValidation"
          aria-describedby="subject-feedback"
        >
        </b-form-input>
        <b-form-invalid-feedback id="subject-feedback"> Campo obrigatório </b-form-invalid-feedback>
      </b-form-group>

    <b-form-group
      label= "Descrição"
      label-for="description"
      >
      <b-form-textarea
      id="description"
      v-model="form.description"
      type="text"
      placeholder="Ex: Pé de alface que ganhei da minha mãe"
      required
      autocomplete="off"
      ></b-form-textarea>
    </b-form-group>

    <b-button
      type="submit"
      variant="outline-primary"
      @click="saveMonitor"
      :disabled="!getValidation"
    > Salvar </b-button>
    </b-form>

  </div>
</template>

<script>
import toastMixin from '@/mixins/toastMixin';
import {required, minLength } from "vuelidate/lib/validators";

export default {
  name: "FormView",

  mixins: [toastMixin],

  data() {
    return{
      form: {
        subject: "",
        description: ""
      },
      methodSave: "new"
    }
  },

  validations: {
    form: {
      subject: {
        required,
        minLength: minLength(3)
      }
    }
  },

  created() {
    if(this.$route.params.index === 0 || this.$route.params.index !== undefined){
      this.methodSave = "update";
      let monitors = JSON.parse(localStorage.getItem("monitors"));
      this.form = monitors[this.$route.params.index];
    }
  },

  methods: {
    saveMonitor() {
      if(this.methodSave === "update"){
        let monitors =  JSON.parse(localStorage.getItem("monitors"));
        monitors[this.$route.params.index] = this.form;
        localStorage.setItem("monitors", JSON.stringify(monitors));
        this.showToast("success", "Sucesso!", "Monitoramento atualizado com sucesso !");
        this.$router.push({ name: "home"});
        return;        
      }

      let monitors = (localStorage.getItem("monitors")) ? JSON.parse(localStorage.getItem("monitors")) : [];
      monitors.push(this.form);
      localStorage.setItem("monitors", JSON.stringify(monitors));
      this.showToast("success", "Sucesso!", "Monitoramento criado com sucesso !");
      this.$router.push({ name: "home"});
    }
  },

  computed: {
    getValidation(){
      if(this.$v.form.subject.$dirty === false) {
        return null;
      }
      return !this.$v.form.subject.$error;
    }
  }
}
</script>

