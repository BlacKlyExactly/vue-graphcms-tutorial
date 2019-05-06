<template>
<div>
    <div class="post" v-for="post in posts" :key="">
       tytuł: {{post.title}}<br/>
       opis:  {{post.description}}<br/>
       data:  {{post.date}}<br/>
    </div>
</div>  
</template>

<script>
const axios = require('axios');
export default {
name : 'Posts',
    data(){
        return{
            posts:[],
        }
    },
    methods:{
        getPosts(){
            axios({
                method: 'post',
                url: 'https://api-euwest.graphcms.com/v1/cjvcmnyen0gce01ghbpurg9yb/master',
                data:{
                    query:`
                       query {
                            posts{
                                title
                                description
                                date
                            }
                         }
                    `,
                }
            })
            .then(res =>{
               this.posts = res.data.data.posts;
            })
        }
    },
    mounted(){
        this.getPosts();
    }
}
</script>

<style lang="scss" scoped>

</style>
