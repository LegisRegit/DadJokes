<template>
    <div class="joke">
    <h3>{{joke.text}}
        <i @click="onBookmark(joke.id, joke.text)" class="fas fa-bookmark"></i>
    </h3>

    </div>
    
</template>


<script>
export default {
    name: 'Joke',
    props: {
        joke: Object
    },
    methods: {
        onBookmark(id, text){
            
            this.$emit('bookmark-joke', id, text)
            
        }
    }
}
</script>

<style scoped>
.fas {
    color: #2F4F4F;
}
.joke {
    background: #f4f4f4;
    margin: 5px;
    padding: 12px 12px;
}
</style>