
<template >
  <v-card>
    <form @submit.prevent="submit" >
      <v-row class="mt-15">
       <v-progress-linear
        v-if="carregando"
        indeterminate
        color="cyan"
      ></v-progress-linear>
        <v-col cols="12" sm="6" md="4">
          <v-text-field
            v-model="cep"
            label="Cep"
            required 
            outlined
            maxlength="8"
          ></v-text-field>
        </v-col>

        <v-col cols="12" sm="6" md="4">
          <v-text-field
            v-model="data.logradouro"
            label="Rua"
            required
            outlined
          ></v-text-field>
        </v-col>

        <v-col cols="12" sm="6" md="4">
          <v-text-field
            v-model="data.localidade"
            label="Cidade"
            required
            outlined
          ></v-text-field>
        </v-col>

        <v-col cols="12" sm="6" md="4">
          <v-text-field
            v-model="data.bairro"
            label="Bairro"
            required
            outlined
          ></v-text-field>
        </v-col>

        <v-col cols="12" sm="6" md="4">
          <v-text-field 
            v-model="data.uf" 
            label="Uf" 
            required  
            outlined
          ></v-text-field>
        </v-col>
      </v-row>

      <v-btn class="my-4" type="submit"> Enviar </v-btn>
      <v-btn class="my-4" @click="clear"> clear </v-btn>
    </form>
  </v-card>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    cep: "",
    data: [{ logradouro: "", localidade: "", bairro: "", uf: "" }],
    carregando: false
  }),

  methods: {
    getCorreio() {
      axios.get(`https://viacep.com.br/ws/${this.cep}/json/`).then((res) => {
        this.carregando =  true
        this.data = res.data;
        setTimeout(() => {
          this.carregando =  false
        }, 700);
         console.log(this.data)
      })
    },
    submit() {
      console.log(this.data);
    },
    clear() {
      this.data = [{ logradouro: "", localidade: "", bairro: "", uf: "" }];
    },
  },

  watch: {
    cep() {
      if (this.cep.length === 8) {
        this.getCorreio();
      }
    },
  },
};
</script>