<template>
  <div>
    <Navegacao />
    <div class="container" style="max-width: 1000px; padding: 30px">
      <h1>Cadastrar novo Local</h1>

      <b-form @submit.prevent="criarUsuario">
        <b-form-group id="input-group-1" label="Nome" label-for="nome">
          <b-form-input
            id="nome"
            v-model="form.nome"
            placeholder="digite o nome do estabelecimento"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Avaliação" label-form="avaliacao">
          <b-form-input
            id="avaliacao"
            v-model="form.avaliacao"
            placeholder="digite sua avaliação"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Rua" label-form="rua">
          <b-form-input
            id="rua"
            v-model="form.rua"
            placeholder="digite a rua do estabelecimento"
            required
          ></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="success"> Criar</b-button>
        <b-button type="reset" variant="danger"> Limpar</b-button>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      form: {
        nome: '',
        avaliacao: '',
        rua: '',
      },
    }
  },
  methods: {
      async criarUsuario(event) {
      event.preventDefault()
      
      try {
         
       let dataLocal = await this.$axios.$post('/lugares/criar', this.form)
        console.log(dataLocal);
        if (dataLocal !== null) {
          this.$bvModal.msgBoxOk('O novo estabelecimento foi cadastrado com sucesso', {
            title: 'Confirmation',
            size: 'sm',
            buttonSize: 'sm',
            okVariant: 'success',
            headerClass: 'p-2 border-bottom-0',
            footerClass: 'p-2 border-top-0',
            centered: true,
          })
          this.limparCampos()
        } else{
          throw new Error(`Não possível cadastrar o estabelecimento ${this.form.nome}`);
        }
      } catch (error) {
        console.log(error);
      }
    },
    limparCampos() {
      this.form = {
        nome: '',
        avaliacao: '',
        rua: '',
      }
    },
  },
}
</script>

<style>
</style>