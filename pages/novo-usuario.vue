<template>
  <div>
    <Navegacao />
    <div class="container" style="max-width: 1000px; padding: 30px">
      <h1>Adcionar novo Usuário</h1>

      <b-form @submit.prevent="criarUsuario">
        <b-form-group id="input-group-1" label="Nome" label-for="nome">
          <b-form-input
            id="nome"
            v-model="form.nome"
            placeholder="digite seu nome"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Email" label-form="email">
          <b-form-input
            id="email"
            v-model="form.email"
            placeholder="digite seu email"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-3" label="Senha" label-form="senha">
          <b-form-input
            id="senha"
            v-model="form.senha"
            placeholder="digite sua senha"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-4" label="Data de Nascimento" label-form="dataNascimento">
          <b-form-input
            id="dataNascimento"
            v-model="form.dataNascimento"
            placeholder="digite sua data de nascimento com barras para espaçar o dia, mês e ano"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-5" label="Gênero" label-form="genero">
          <b-form-input
            id="genero"
            v-model="form.genero"
            placeholder="digite seu gênero"
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
        email: '',
        senha: '',
        dataNascimento: '',
        genero: '',
      },
    }
  },
  methods: {
      async criarUsuario(event) {
      event.preventDefault()
      
      try {
        
       let dataUsuario = await this.$axios.$post('/usuarios/cadastrar', this.form)
        console.log(dataUsuario);
        if (dataUsuario !== null) {
          this.$bvModal.msgBoxOk('O novo usuário foi cadastrado com sucesso', {
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
          throw new Error(`Não possível cadastrar o usuário ${this.form.nome}`);
        }
      } catch (error) {
        console.log(error);
      }
    },
    limparCampos() {
      this.form = {
        nome: '',
        email: '',
        senha: '',
        dataNascimento: '',
        genero: '',
      }
    },
  },
}
</script>

<style>
</style>