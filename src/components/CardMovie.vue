<template>
<li>
    <h3>{{movie.title}}</h3>
    <p>{{movie.original_title}}</p>
    <p>{{movie.original_language}}</p>
    <p>{{movie.vote_average}}</p>
</li>

</template>


<script>
    export default{
        props:{
            movie:{
                type: Object,
                require: true
            }
        }
    }


</script>

<style lang="scss" scoped>

</style>