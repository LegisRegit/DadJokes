<template>
    <h1 id="randomjoke">{{ title }}</h1>

    <Button @click="search()" text="New Joke" color="green"/>

    <Jokes @bookmark-joke="bookmarkJokeForward" :jokes="jokes" />

</template>

<script>
import Button from './Button'
import Jokes from './Jokes'

export default {
    name: 'Random',
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
      fetch("https://icanhazdadjoke.com/", {
          method: "GET",
          headers: {"Accept": "application/json"},

      }).then(
        res => {
          res.json().then(data => {
            
                this.jokes.push({text: data.joke, id: data.id});
                
            
          });
        }
      );
      
    }
  },

    emits: ['bookmark-joke']

}
</script>
