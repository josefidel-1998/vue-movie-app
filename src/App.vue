<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movie</h1>
    </router-link>
  </header>
  <main>
  </main>
  <router-view></router-view>
</template>

<style lang="scss">
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;

      &::selection{
         background: transparentize(#428883,0.5);
      }
  }
  body{
    background-color: #35495b;
  }
  a{
    text-decoration: none;
  }
  header{
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #2c3d4e;
    padding: 0.8rem 1rem;
    box-shadow: 0,0,6px, rgba(0,0,0,0.1);
      h1{
        color: white;
        font-size: 1.8rem;
        span{
          color: #2a445f;
        }
      }
  }

</style>
