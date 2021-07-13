<template>  
  <div>
  <main class="page-content" aria-label="Content">
    <div class="wrapper">
    <div class="home">
      <h1 class="page-heading" v-if="page.title">{{ page.title }}</h1>
  
      <slot name="default"></slot>
      
      <hr />

      <h2
        class="post-list-heading"
        v-if="page.posts && page.posts.length > 0"
      >{{ page.listTitle || 'Posts' }}</h2>
  
      <ul class="post-list" v-if="page.posts && page.posts.length > 0">
        <li v-for="post in page.posts" :key="post.permalink">
          <span class="post-meta">{{ formatDate(post.createdAt) }}</span>
          <h3>
            <saber-link
              class="post-link"
              :to="post.permalink"
            >{{ post.title }}</saber-link>
          </h3>
        </li>
      </ul>
  
      <div
        class="pagination"
        v-if="page.pagination && (page.pagination.hasNext || page.pagination.hasPrev)"
      >
        <router-link
          class="prev-link"
          :to="page.pagination.prevLink"
          v-if="page.pagination.hasPrev"
        >← Previous</router-link>
        <router-link
          class="next-link"
          :to="page.pagination.nextLink"
          v-if="page.pagination.hasNext"
        >Next →</router-link>
      </div>
      
      <!-- The RSS Subscribe button

      <p class="feed-subscribe" v-if="feedLink">
        <svg class="svg-icon orange">
          <use :xlink:href="getSvg('rss')"></use>
        </svg>
        <a :href="feedLink">Subscribe</a>
      </p>
      
      -->
    </div>
    </div>
    <Footer :siteTitle="siteTitle"/>
    </main>
  </div>
</template>

<script>
import formatDate from '../utils/formatDate';
import Footer from '../components/Footer.vue';
import getSvg from '../utils/getSvg';
export default {
  components: {
    Footer: Footer
  },
  props: ['page'],
  computed: {
    feedLink: function feedLink() {
      return this.$feed && this.$feed.permalink;
    },
    siteTitle: function siteTitle() {
      return this.$siteConfig.title || 'Your Awesome Title';
    }
  },
  methods: {
    formatDate: formatDate,
    getSvg: getSvg
  }
};
</script>
