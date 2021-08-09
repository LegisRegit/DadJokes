<template>
    <div :key="joke.id" v-for="joke in jokes">
        <Joke @bookmark-joke="bookmarkJokeForward(joke.id, joke.text)" :joke="joke" />
    </div>
</template>


<script>
import Joke from './Joke'

export default {
    name: 'Jokes',
    props: {
        jokes: Array
    },
    components : {
        Joke,
    },
    methods: {
    bookmarkJokeForward(id, text){
        this.$emit('bookmark-joke', id, text);
    }
    },
    emits: ['bookmark-joke']
}
</script>