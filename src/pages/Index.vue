<template>
  <Layout>
    <h1 class="text-center h5 font-family-sans-serif mb-5"></h1>
    <Post :post="node" v-for="{ node } in $page.allWordPressPost.edges" :key="node.id"/>
    <Pagination :info="$page.allWordPressPost.pageInfo"/>
  </Layout>
</template>

<page-query>
query Home($page: Int) {
  allWordPressPost(page: $page, perPage: 10) @paginate {
    pageInfo {
      totalPages
      currentPage
    }
    edges {
      node {
        date
        id
        title
        path
        content
        excerpt
        categories {
          id
          title
          path
        }
        author {
          name
          path
        }
      }
    }
  }
}
</page-query>

<script>
import Post from '~/components/Post.vue'
import Pagination from '~/components/Pagination.vue'

export default {
  components: {
    Post,
    Pagination
  },
  metaInfo: {
    title: 'Recent projects I have enjoyed working on.'
  }
}
</script>
