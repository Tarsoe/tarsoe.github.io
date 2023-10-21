<template>
  <div>
    <b-row>
      <b-col v-for="post in posts" :key="post.slug">
        <b-card :title="post.title" tag="article" style="max-width: 20rem;" class="mb-2">
          <b-card-text>
            {{ post.description }}
          </b-card-text>
          <b-button :to="{ name: 'posts-slug', params: { slug: post.slug } }" variant="primary">Go somewhere</b-button>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const postsData = await $content('posts').fetch()
    // return {
    //   posts: postsData,
    // };
    // Sort the posts by slug with leading zeros
    const sortedPosts = postsData.sort((a, b) => {
      console.log("a.slug = ", a);
      console.log("b.slug = ", b.slug);
      console.log("a.slug.localeCompare = ", a.slug.localeCompare());
      console.log("a.slug.localeCompare(b.slug) = ", a.slug.localeCompare(b.slug));
      console.log("a.slug.localeCompare(b.slug, undefined) = ", a.slug.localeCompare(b.slug, undefined));
      console.log("a.slug.localeCompare(b.slug, undefined, { numeric: true, sensitivity: 'base' }); = ", a.slug.localeCompare(b.slug, undefined, { numeric: true, sensitivity: 'base' }));
      // return a.slug.localeCompare(b.slug, undefined, { numeric: true, sensitivity: 'base' });
      // return a.slug.localeCompare(); 
      return (-1); 
    });
    return {
      posts: sortedPosts,  // Use the sorted array
    };
  },
  mounted() {
    console.log("This.posts = ", this.posts);
  }
}
</script>

<style lang="scss" scoped></style>