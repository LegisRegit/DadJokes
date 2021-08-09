<template>
    <h1 id="findjoke">{{ title }}</h1>
    

    <div class="form-inline p-5">
      Search Term:
      <br>
      <div class="form-group">
        <input class="form-control" type="text" v-model="term">
      </div>
    </div>

    <div id="noResults">No results, sorry ;n;</div>
    
    <Button @click="search()" text="Go" color="green"/>

    <Jokes @bookmark-joke="bookmarkJokeForward" :jokes="jokes" />

</template>

<script>
import Button from './Button'
import Jokes from './Jokes'

export default {
    name: 'Search',
    props: {
        title: String,
    },
    components: {
        Button,
        Jokes,
    },
    data() {
    return {
      jokes: [],
      term: "",
    }
    },
    

    methods: {
    bookmarkJokeForward(id, text){
        this.$emit('bookmark-joke', id, text);
    },

    search() {
        while (this.jokes.length > 0){
            this.jokes.pop();
        }
      fetch("https://icanhazdadjoke.com/search?limit=10&term=" + this.term, {
          method: "GET",
          headers: {"Accept": "application/json"},

      }).then(
        res => {
          res.json().then(data => {
            data.results.forEach(element => {
                var newjoke = element.joke;
                var newid = element.id;
                this.jokes.push({text: newjoke, id: newid});
                
            });
            console.log(data)
            if (this.jokes.length > 0) {
                    document.getElementById("noResults").style.visibility = "hidden";
                } 
                if (this.jokes.length < 1) {
                    document.getElementById("noResults").style.visibility = "visible";
                }
          });
        }
      );
      
    }
  },

    emits: ['bookmark-joke']

}
</script>
