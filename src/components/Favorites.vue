<template>
    <h1 id="favorites">{{ title }}</h1>

    <Jokes @bookmark-joke="bookmarkJokeForward" :jokes="jokes" />

</template>

<script>
import Jokes from './Jokes'

export default {
    name: 'Favorites',
    props: {
        saved: Array,
        title: String,
    },
    components: {  
        Jokes,
    },
    data() {
    return {
      jokes: this.saved,
    }
    },
    

    methods: {
    bookmarkJokeForward(id, text){
        this.$emit('bookmark-joke', id, text)
    },
    
  },

    emits: ['bookmark-joke']

}
</script>