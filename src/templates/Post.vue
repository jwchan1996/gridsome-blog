<template>
  <Layout>
    
    <!-- Page Header -->
    <header class="masthead" :style="{ backgroundImage: `url(http://localhost:1337${$page.post.cover.url})`}">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-heading">
              <h1>{{ $page.post.title }}</h1>
              <!-- <h2 class="subheading">Problems look mighty small from 150 miles up</h2> -->
              <span class="meta">Posted by
                <a href="#">{{ $page.post.user.username }}</a>
                on {{ $page.post.created_at }}</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Post Content -->
    <article>
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto" v-html="mdToHTML($page.post.content)">
          </div>
        </div>
      </div>
    </article>

  </Layout>
</template>

<page-query>
query ($id: ID!) {
  post: strapiPost (id: $id) {
    id
    title
    content
    cover {
      url
    }
    tags {
      id
      title
    }
    user {
      id
      username
    }
    created_at
  }
}
</page-query>

<script>
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt()

export default {
  name: 'HomePage',
  metaInfo: {
    title: 'Hello World!'
  },
  methods: {
    mdToHTML(markdown) {
      return md.render(markdown)
    }
  }
}
</script>

<style>

</style>