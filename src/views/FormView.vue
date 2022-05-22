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
          placeholder="(Mínimo de 3 caracteres)"
          required
          autocomplete="off"
          :state="getValidation"
          aria-describedby="subject-feedback"
        >
        </b-form-input>
        <b-form-invalid-feedback id="subject-feedback"> Campo obrigatório </b-form-invalid-feedback>
      </b-form-group>

    <b-form-group
      label= "Selecione uma planta"
      label-for="plants"
      >
      <b-form-select
      id="plants"
      v-model="form.plants"
      :options="optionsList"
      required
      ></b-form-select>
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
        plants:"",
        description: ""
      },
      methodSave: "new",
        optionsList: [
          { value: "Ervilha", text: "Ervilha" },
          { value: "Cenoura", text: "Cenoura" },
          { value: "Abobrinha", text: "Abobrinha" },
          { value: "Beterraba", text: "Beterraba" },
          { value: "Alface", text: "Alface" },
          { value: "Vagem", text: "Vagem" },
          { value: "Cebolinha", text: "Cebolinha" },
          { value: "Acelga", text: "Acelga" },
          { value: "Tomate", text: "Tomate" },
          { value: "Pepino", text: "Pepino" },
          { value: "Espinafre", text: "Espinafre" },
          { value: "Rabanete", text: "Rabanete" }
        ]
    }
  },

  validations: {
    form: {
      subject: {
        required,
        minLength: minLength(3)
      },
      plants: {
        required
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
      this.$v.$touch();
      if(this.$v.$error) return;

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

