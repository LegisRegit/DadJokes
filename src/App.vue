<template>
  <div id="app">
    <nav class="navbar navbar-expand navbar-dark fixed-top" id="mainNav">
    <div class="container">
      <!-- Header -->
      <header class="masthead">
      <Header title="Dad Jokes" />
      </header>

      
      <div class="collapse navbar-collapse" id="navbarResponsive">
        <ul class="navbar-nav text-uppercase ml-auto">          
          <li class="nav-item">
            <a class="nav-link js-scroll-trigger" href="#findjoke">Search for a Joke</a>
          </li>
          <li class="nav-item">
            <a class="nav-link js-scroll-trigger" href="#randomjoke">Random Joke</a>
          </li>
          <li class="nav-item">
            <a class="nav-link js-scroll-trigger" href="#favorites">Favorites</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
<div class="container">

 <!-- Find a Joke -->

  <div class="container"> 
    <Search @bookmark-joke="bookmarkJoke" title="Search For a Joke" />
  </div>
 

 

  <!-- Random Joke -->

   <div class="container">
     <Random @bookmark-joke="bookmarkJoke" title="A Random Joke" />
   </div>

  
  <!-- Favorites -->

  <div class="container">
    <Favorites @bookmark-joke="bookmarkJoke" title="Your Favorites" :saved="bookmarks"/>
  </div>

</div>
  


 

  
  </div>
</template>

<script>
import Favorites from './components/Favorites'
import Header from './components/Header' 
import Search from './components/Search'
import Random from './components/Random'

export default {
  name: 'App',
  components: {
    Header,
    Search,
    Favorites,
    Random,
  },
  data() {
    return {
      bookmarks: [],
    }
    },
  methods: {
    bookmarkJoke(id, text){
        var index = -1;
        for(var i = 0, len = this.bookmarks.length; i < len; i++) {
          if (this.bookmarks[i].id === id) {
          index = i;
          break;
         } 
      
      }
      if (index != -1) {
        this.bookmarks.splice(index, 1);
        index = -1;
      }
      else {this.bookmarks.push({"id": id, "text": text});
      }
      console.log(this.bookmarks);
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 5px;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
