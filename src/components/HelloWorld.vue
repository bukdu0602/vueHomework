<template>
  <div class="hello">

    <h1>Artist Directory</h1>
    <div class="artistBox">
      <input  type="text" v-on:input="runFilter()" v-model="filter"><br />
      <button class="addButton" v-on:click="showInputBoxes">Add artist</button>
    </div>

    <div class="artistInputs" v-if="addButtonPressed">
        <input placeholder="Artist Name" type="text" v-model="artistName"><br />
        <input placeholder="About artist" type="text" v-model="aboutArtist"><br />
        <input placeholder="Image url" type="text" v-model="url"><br />
        <button class="addButton" v-on:click="addArtist(artistName, aboutArtist, url)">Add</button>
    </div>

    <div v-if="artistsArray.length > 0 && !filter">
      <div class="artistCard" v-for="artist in artistsArray" :key="artist.id">
        <img :src="artist.url" alt="">
        <span>
        <p>{{artist.name}}</p>
        <p>{{artist.about}}</p>
        </span>
        <button class="deleteButton" v-on:click="deleteBtn(artist.id)">Delete</button>
      </div>
    </div>

<div v-if="filter">
      <div class="artistCard" v-for="f in filtered" :key="f.id">
        <img :src="f.url" alt="">
        <span>
        <p>{{f.name}}</p>
        <p>{{f.about}}</p>
        </span>
        <button class="deleteButton" v-on:click="deleteBtn(f.id)">Delete</button>
      </div>
    </div>
      



  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      addButtonPressed: false,
      artistsArray: [],
      idNum: 0,
      filter: "",
      filtered: []
    }
  },
  methods: {
    runFilter(){
    this.filtered = this.artistsArray.filter(item => item.name.includes(this.filter))
    console.log(this.filter)
    },
    showInputBoxes() {
      console.log("hlhl")
      this.addButtonPressed = true
    },
  addArtist(artistName, aboutArtist, url) {
    const artist = {
      id: this.idNum,
      name: artistName,
      about: aboutArtist,
      url: url
    }
    this.artistsArray.push(artist)
    this.idNum++
    console.log(this.idNum)
        console.log(this.artistsArray)

  },
  deleteBtn(id) {
    console.log(id)
    for(let i=0; i<this.artistsArray.length; i++){
      if (id == this.artistsArray[i].id){
        this.artistsArray.splice(i, 1) 
      }
    }
    // 
   
  }
  }
}
</script>

<style scoped>

.artistBox {
  display: flex;
}
.box{
  width: 500px;
  height: 40px;
  border: solid 1px rgb(204, 204, 204);
  border-radius: 5px;
 
}
.addButton {
    margin-left: 10px;
    padding: 5px;
    font-size: 1.5em;
    border: none;
  }
.artistInputs {
}
.artistCard {
  display: flex;
  justify-content: space-between;
}
</style>
