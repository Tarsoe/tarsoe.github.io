<template>
    <div>
        <b-img v-if="post.image" :src="post.image"></b-img>
        <h1>{{ post.title }}</h1>
        <p>{{ post.description }}</p>
        <hr>
        <nuxt-content :document="post"></nuxt-content>
    </div>
</template>

<script>
export default {
    async asyncData({ $content, params }) {
        const postData = await $content('posts', params.slug).fetch();
        return {
            post: postData,
        };
    },
    mounted() {
        console.log("In _slug.vue This.post", this.post);
    }
}
</script>

<style lang="scss" scoped></style>