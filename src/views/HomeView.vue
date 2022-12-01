<template>
  <div id="background">
    <h1>Jukebox</h1>
    <div id="nav-menu">
      <h2>All Songs</h2>
      <h2 id="unactive" @click="redirect('/playlists')">Playlists</h2>
    </div>

    
    
  </div>

</template>

<script>

  export default {
    name: 'Home',
    data () {
      return {

        songs: [
              {
                SongName: 'Dancing Queen',
                Artist: 'ABBA',
                fileName: 'dancingQueen.mp3'
              },
              {
                SongName: 'Mamma Mia',
                Artist: 'ABBA',
                fileName: 'mammaMia.mp3'
              },
              {
                SongName: 'ABC',
                Artist: 'The Jackson 5',
                fileName: 'abc.mp3'
              },
              {
                SongName: 'Mr. Blue Sky',
                Artist: 'Electric Light Orchestra',
                fileName: 'blueSky.mp3'
              },
              {
                SongName: 'I Want You Back',
                Artist: 'The Jackson 5',
                fileName: 'wantYouBack.mp3'
              },
              {
                SongName: 'Hooked On A Feeling',
                Artist: 'Blue Swede, Bjorn Skifs',
                fileName: 'hookedOnAFeeling.mp3'
              },
              {
                SongName: 'Spirit in the Sky',
                Artist: 'Norman Greenbaum',
                fileName: 'spiritInTheSky.mp3'
              },
              {
                SongName: 'Aint No Mountain High Enough',
                Artist: 'Marvin Gaye, Tammi Terrell',
                fileName: 'mountain.mp3'
              },
              {
                SongName: 'Come And Get Your Love',
                Artist: 'Redbone',
                fileName: 'yourLove.mp3'
              },
              {
                SongName: 'Escape (The Pina Colada Song)',
                Artist: 'Rupert Holmes',
                fileName: 'escape.mp3'
              },
              {
                SongName: 'O-o-h Child',
                Artist: 'The Five Stairsteps',
                fileName: 'oohChild.mp3'
              },
              {
                SongName: 'The Boys Are Back In Town',
                Artist: 'Thin Lizzy',
                fileName: 'boysBack.mp3'
              }
            ],

      }
    },
    created(){
      localStorage.setItem("songs", JSON.stringify(this.songs));
    },
    methods: {
      redirect(x){
        this.$router.push(`/${x}`);
      }
    }

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
#unactive{
  color: #EF8382;
}
</style>
