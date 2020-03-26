<template>
  <div id="app">
    <h1>{{ message }}</h1>
    <div class="input">
      <input type="hidden" name="index" v-model="tempIndex">
      <label>URL :</label>
      <input type="text" name="url" v-model="tempUrl">
      <label>NAME :</label>
      <input type="text" name="name" class="name_input" v-model="tempName">
      <label>DESC :</label>
      <input type="text" name="desc" class="desc_input" v-model="tempDesc">
      <input type="submit" name="submit" value="SUBMIT" v-on:click="addImage">
      <input type="submit" name="submit" value="DELETE" v-on:click="deleteImage">
    </div>
    <br>  
    <br>  
    <div class="gallery">
      <div>
        <button id="prev" @click="prev">PREV</button>
        <img v-bind:src="items[tempIndex].url" style="max-width: 900px">
        <button id="next" @click="next">NEXT</button>
      </div>
      <div>
        <h1>{{items[tempIndex].name}}</h1>
        <p>{{items[tempIndex].desc}}</p>
      </div>
      <hr>
      <div>
        <span class="thumbnail-list" v-for="(item, index) in items" @click="selectImage(index)">
          <img v-bind:src="item.url" class="thumbnail">
          <h5>{{item.name}}</h5>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      message: 'Doggo Gallery',
      tempUrl: '',
      tempName: '',
      tempDesc: '',
      tempIndex: 0,
      items: [
        { name: 'Mommy and Me',
          desc: 'Was a beautiful live we have, every morning was an amazing day',
          url: 'https://www.sciencemag.org/sites/default/files/styles/article_main_large/public/dogs_1280p_0.jpg?itok=cnRk0HYq' },
        { name: 'Bad Day',
          desc: 'Was a bad day to talk about',
          url: 'https://www.iamexpat.nl/sites/default/files/styles/article--full/public/dog-on-leash-walking-on-grass.jpg?itok=xbF_5H3u' },
        { name: 'Sunshine',
          desc: 'Live is good when you can to the best everyday and stay lookup',
          url: 'https://d17fnq9dkz9hgj.cloudfront.net/breed-uploads/2018/08/alaskan-malamute-card-medium.jpg?bust=1535569398' }      
      ]
    }
  },
    methods: {
      addImage(){
        this.items.push({name: this.tempName, url: this.tempUrl , desc: this.tempDesc});
        this.tempName='';
        this.tempUrl='';
        this.tempDesc='';
      },
      deleteImage(){
        if(this.tempIndex!=0){
          this.items.splice(this.tempIndex, 1);
          this.tempIndex--;
          this.tempUrl='';
          this.tempName='';
          this.tempDesc='';
        }
      },
      selectImage(index){
        this.tempName=this.items[index].name;
        this.tempUrl=this.items[index].url;
        this.tempDesc=this.items[index].desc;
        this.tempIndex=index;
      },
      prev(){
        if(this.tempIndex > 0) this.tempIndex--;
      },
      next(){
        if(this.tempIndex < this.items.length-1) this.tempIndex++;
      }      
    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.thumbnail{
  max-width: 200px;
}

.thumbnail-list{
  display: inline-block;
  margin: 10px;
}
</style>
