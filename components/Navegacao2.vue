<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">BLOOMIS</b-navbar-brand>

      <b-navbar-nav class="ml-auto">
        <b-nav-form>
          <b-button to="/novo-usuario" size="sm" class="mr-sm-2">
            Novo Usuário
          </b-button>
        </b-nav-form>

        <b-nav-form>
          <b-button to="/_locais" size="sm" class="mr-sm-2">
            Lista de Locais
          </b-button>
        </b-nav-form>
      </b-navbar-nav>
    </b-navbar>

  </div>
</template>