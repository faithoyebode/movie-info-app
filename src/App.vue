<template>
  <div class="App">
    <header>
      <router-link to='/'>
        <h1>Movie Info App</h1>
      </router-link>
    </header>
    <main>
      <router-view />
    </main>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;

  &::selection{
    background: transparentize(#E50914, 0.5);
  }
}

body{
  
}

.App{
  max-width: 700px;
  margin-left: auto;
  margin-right: auto;
  background-color: #1f1f1f;
  min-height: 100vh;
}

a{
  text-decoration: none;
}

header{
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #141414;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
  position: fixed;
  width: 100%;
  max-width: 700px;
  z-index: 10;

  h1{
    color: #FFFFFF;
    font-size: 28px;
    

    span{
      color: #42b883;
    }
  }
}
</style>
