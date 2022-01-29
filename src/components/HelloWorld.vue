<template>
  <div class="hello">

    
    <div class="artistBox">
      <h1>Artist Directory</h1>
      <div>
      <input class="filterInput"  type="text" v-on:input="runFilter()" v-model="filter"><br />
      <button class="addButton" v-on:click="showInputBoxes">Add artist</button>
      </div>
    </div>

    <div class="artistInputs" v-if="addButtonPressed">
        <input placeholder="Artist Name" type="text" v-model="artistName"><br />
        <input placeholder="About artist" type="text" v-model="aboutArtist"><br />
        <input placeholder="Image url" type="text" v-model="url"><br />
        <div class="artistButton">
        <button class="addButton2" v-on:click="addArtist(artistName, aboutArtist, url)">Add</button>
        </div>
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
    this.addButtonPressed = false
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
    margin: auto;
    border: solid 1px silver;
    padding: 20px;
    max-width: 600px;
    
}
.artistBox div{
    display: flex;
}
.filterInput {
    width: 500px;
    height: 30px;
}
.addButton {
    margin-left: 5px;
}

.artistInputs {
    margin: auto;
    width: 400px;
}
.artistInputs input{
   width: 100%;
   height: 30px;
    text-align: center;
}

.artistButton {
    margin: auto;
    width: 200px;
}
.artistInputs button {
    width: 100%;
    height: 30px;

}

.artistCard {
    border: solid 1px silver;
    display: grid;
    grid-template-columns: 1fr 4fr 1fr;
    grid-template-areas: "pic  contents  delete";
    padding: 5px;
    max-width: 600px;
    margin: 10px auto;

}

.artistCard img {
    grid-area: pic;
    display: block;
    width: 70%;
    border-radius: 5px;
}
.artistCard span {
    grid-area: contents;
}
.artistCard button{
    grid-area: delete;
    width: 50%;
    height: 30%;
    margin: auto;
    background-color: red;
    color: white;
    border: none;
    border-radius: 5px;
}

</style>
