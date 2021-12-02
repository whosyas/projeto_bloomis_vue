<template>
<div>
    <Navegacao3 />
      <div class="container">
      <h1>Locais da cidade:</h1>
      <b-table striped responsive hover :items="locais" :fields="campos">
        <template v-slot:cell(categoria)="data">
          <b-icon class="h2 mb-2" :icon="data.value"></b-icon>
        </template>

        <template #cell(locais)="data">
          <NuxtLink :to="`/listas/${data.item.id}`">
            <span>{{ data.value }}</span>
          </NuxtLink>
        </template>
      </b-table>
      <div>
        <b-button to="/_novo-local" pill variant="info">
          <b-icon icon="plus"></b-icon>
        </b-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    let locais
    try {
      locais = await $axios.$get('/lugares')
      // data = response.data
    } catch (e) {
      console.log(e)
    }
    console.log(JSON.stringify(locais));
    return { locais }
  },

  data: () => {
    return {
      campos: [
        {
          key: 'nome',
        },

        {
          key: 'avaliacao',
        },

        {
          key: 'rua',
        },
      ],
    }
  },
}
</script>
