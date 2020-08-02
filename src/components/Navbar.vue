<template>
  <nav class="navbar is-danger" role="navigation" aria-label="main navigation">
        <div class="navbar-brand">
          <a class="navbar-item" id="logo" href="https://bulma.io">
            <img id="pokebola" src="../assets/pokemon.svg" alt="pokebola">
            Pokedex
          </a>

          <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
          </a>
        </div>

        <div id="navbarBasicExample" class="navbar-menu">
          <div class="navbar-start">
            <a class="navbar-item">Home</a>
            <a class="navbar-item">Documentation</a>
            <a class="navbar-item">Pokemons</a>
          </div>

          <div class="navbar-end">
            <div class="navbar-item">
              <div class="buttons">
                <a class="button is-light"><strong>Sign up</strong></a>
                <a class="button is-light">Log in</a>
              </div>
            </div>
          </div>
        </div>
      </nav>
</template>

<script>
export default {

}
</script>

<style>
    #logo {
        margin: 0 30px;
    }

    #logo img {
        margin-right: 10px;
    }
</style>