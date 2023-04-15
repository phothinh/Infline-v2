<template>
  <div class="px-[5vw] py-[2vw] mb-[5vw]">
    <h3 class="text-left text-[3.5vw] text-infline-black font-integral uppercase ml-[3.4vw] mt-[2vw]">Les news</h3>
    <div class="flex items-center justify-center mt-[3vw] ">
      <BlogPost v-for="(article, index) in articles" :key="index"
        :date="formatDate(article.attributes.date)"
        :description="article.attributes.title"
        :imageUrl="article.attributes.image.data.attributes.url"
        class="mx-[2vw]"
      />
    </div>
  </div>
</template>

<script>
import BlogPost from "~/components/BlogPost";
import gql from 'graphql-tag'

export default {
  components: {
    BlogPost,
  },
  methods: {
    formatDate(dateStr) {
      return new Date(dateStr);
    }
  },
  apollo: {
    articles: {
      query: gql`
        query allArticlesQuery {
          articles {
            data {
              id
              attributes {
                title
                slug
                description
                body
                date
                image {
                  data {
                    attributes {
                      url
                    }
                  }
                }
              }
            }
          }
        }
      `,
      update: (data) => {
        return data.articles.data.slice(0, 3)
      }
    }
  }
}
</script>
