<template>
  <div id="background">
    <h1>Jukebox</h1>
    <div id="nav-menu">
      <h2 id="unactive" @click="redirect('')">All Songs</h2>
      <h2>Playlists</h2>
    </div>

    <div id="cont">
      <v-card v-for="(playlist, index) in playlists" v-bind:key="index" class="playlistCard">
        <h3>{{playlists[index].playlistName}}</h3>
        <h4>{{playlists[index].description}}</h4>
      </v-card>

    </div>

    <v-btn
      color="#3097F3"
      fab
      dark
      id="fab-btn"
      @click="createNew()"
      >
      <v-icon id="fab-icon">mdi-plus</v-icon>
    </v-btn>

    <v-dialog
      v-model="dialog"
      width="50%"
      height="50%"
      >
      <v-card id="newFlex" class="scrollOverflow">
        <div id="head">
          <input type="text" value="playName" v-model="PlayName" placeholder="Playlist Name" id="newHead">
          <input type="text" value="playDesc" v-model="PlayDesc" placeholder="Playlist Description" id="newSub">
        </div>
        
        <v-divider></v-divider>
        <div v-for="(song, index) in songs" v-bind:key="index" class="rowFlex">
          <div class="colFlex">
            <h5>{{songs[index].SongName}}</h5>
            <h6>{{songs[index].Artist}}</h6>
            <v-divider class="newdiv"></v-divider>
          </div>
          <div></div>
        </div>
      </v-card>

    </v-dialog>
    
  </div>

</template>

<script>

  export default {
    name: 'Playlist',
    data () {
      return {
        dialog: false,
        PlayName: '',
        PlayDesc: '',
        Selected: [],
        playlists: [
          {
            playlistName: 'Geez Marty, When Are We',
            description: 'rewind with a flash from the past',
            songs: ['Mr. Blue Sky', 'I Want You Back', 'Hooked On A Feeling', 'Spirit in the Sky', 'Aint No Mountain High Enough']
          },
          {
            playlistName: 'Doc I Think We Miss Calculated',
            description: 'rewind with a flash from the past, again',
            songs: ['Come And Get Your Love', 'Escape (The Pina Colada Song)', 'O-o-h Child', 'The Boys Are Back In Town', 'Dancing Queen', 'Mamma Mia', 'ABC']
          }
        ],
        songs: []

      }
    },
    created(){
      var x = JSON.parse(localStorage.getItem("songs"));
      if (x == null || x == "") {
        x = [];
      }
      this.songs = x;
    },
    methods: {
      redirect(x){
        this.$router.push(`/${x}`);
      },
      createNew(){
        this.dialog = true;
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
#cont{
  margin: 5% 20%;
}
.playlistCard{
  margin-bottom: 3%;
  height: 120px;
}
h3{
  font-family: 'lato-bold';
  font-size: 24px;
  padding: 25px 35px 10px 35px;
}
h4{
  font-family: 'lato';
  font-size: 16px;
  padding: 0px 35px 25px 35px;
}
#fab-btn{
  position: fixed;
  bottom: 5%;
  right: 15%;
  width: 100px;
  height: 100px;
}
#fab-icon{
  width: 75px;
  height: 75px;
  font-size: 75px;
}
#newHead{
  font-family: 'lato-bold';
  font-size: 24px;
}
#newSub{
  font-family: 'lato';
  font-family: 16px;
}
#newFlex{
  display: flex;
  flex-direction: column;
}
#head{
  margin: 40px 60px;
  display: flex;
  flex-direction: column;
}
.rolFlex{
  display: flex;
  flex-direction: row;
}
.colFlex{
  display: flex;
  flex-direction: column;
  padding-left: 60px;
}
h5{
  font-family: 'lato';
  font-size: 24px;
  color: #0360D9;
}
h6{
  font-family: 'lato';
  font-size: 16px;
  color: #0360D9;
}
.scrollOverflow {
  overflow: scroll;
}
.newdiv{
  margin-top: 10px;
  margin-bottom: 10px;
}
</style>
