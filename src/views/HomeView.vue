<template>
  <main class="home-page">
    <h1>Home</h1>
    <p>This is home page</p>
  </main>
</template>

<style lang="scss" >
  body{
    background-image: linear-gradient(to bottom,#563E24, rgba(0, 0, 0, 0.986));
    font-family:system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
  .player{
    background-image: url("../assets/img/player_background.svg");
    max-width: 1170px;
    max-height: 170px;
    object-fit: cover;
    margin: auto;
    font-size: 20px;
    color: white;
    box-shadow:  10px 10px 4px 7px rgba(0, 0, 0, 0.25), inset 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
    text-align: center;
  }
  button{
    background: none;
    border: none;
    margin: 30px;
    margin-top: 0px;
    margin-bottom: 10px ;
  }

  .album-cover{
    max-width: 100px;
    max-height: 100px;
  }
</style>

