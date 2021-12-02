<template>
  <div>
    <Navegacao2 />
    <div class="container">
      <h1>Usuários:</h1>
      <b-table striped responsive hover :items="usuarios" :fields="campos">
        <template v-slot:cell(categoria)="data">
          <b-icon class="h2 mb-2" :icon="data.value"></b-icon>
        </template>

        <template #cell(locais)="data">
          <NuxtLink :to="`/listas/${data.item.id}`">
            <span>{{ data.value }}</span>
          </NuxtLink>
        </template>
      </b-table>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    let usuarios
    try {
      usuarios = await $axios.$get('/usuarios')
      // data = response.data
    } catch (e) {
      console.log(e)
    }
    console.log(JSON.stringify(usuarios));
    return { usuarios }
  },

  data: () => {
    return {
      campos: [
        {
          key: 'nome',
        },

        {
          key: 'email',
        },

        {
          key: 'dataNascimento',
        },

        {
          key: 'genero',
        },
        
      ],
    }
  },
}
</script>
