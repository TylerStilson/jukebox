<template>
  <div id="background">
    <h1>Jukebox</h1>
    <div id="nav-menu">
      <h2>All Songs</h2>
      <h2>Playlists</h2>
    </div>
    
  </div>

</template>

<script>

  export default {
    name: 'Home',

  }
</script>

<style scoped>
#background{
  background-image: url('../assets/images/background.svg');
  width: 100vw;
  height: 100vh;
  background-size: cover;
}
h1{
  font-family: 'baloo-bold';
  color: white;
  font-size: 200px;
  width: 100%;
  text-align: center;
  padding-top: 2%;
}
h2{
  font-family: 'baloo';
  color: #D90504;
  font-size: 24px;
}
#nav-menu{
  display: flex;
  justify-content: space-around;
  margin: 0px 40%;
}
</style>
