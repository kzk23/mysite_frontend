<template>
  <div>
    <h1 class="title">ブログの投稿</h1>
    <form-post v-model="post" @save="save" @reset="reset" />
    <hr />
    <list-posts v-model="posts" @remove="remove" @loadPost="loadPost" />
  </div>
</template>

<script>
import ListPosts from '@/components/ListPosts'
import FormPost from '@/components/FormPost'
export default {
  components: { FormPost, ListPosts },
  async fetch() {
    this.posts = await this.$axios.$get('/api/posts')
  },
  data() {
    return {
      posts: [],
      post: {
        creation_at: new Date().toISOString(),
      },
    }
  },
  methods: {
    async save() {
      const method = this.post.id ? 'put' : 'post'
      const id = this.post.id ? `${this.post.id}/` : ''
      const url = `/api/posts/${id}`
      try {
        await this.$axios[method](url, this.post)
        this.$toasted.global.defaultSuccess({
          msg: 'Operação realizada com sucesso',
        })
        this.$fetch()
      } catch (err) {
        for (const item in err.response.data) {
          this.$toast.error(item + ': ' + err.response.data[item])
        }
      }
    },
    loadPost(post) {
      this.post = {
        id: post.id,
        text: post.text,
        created_at: post.created_at,
      }
    },
    async remove(post) {
      const url = `/api/posts/${post.id}`
      try {
        await this.$axios.$delete(url)
        this.$toasted.global.defaultSuccess({
          msg: 'Questão removida com sucesso',
        })
        this.$fetch()
      } catch (err) {
        for (const item in err.response.data) {
          this.$toast.error(item + ': ' + err.response.date[item])
        }
      }
    },
    reset() {
      this.post = {
        created_at: new Date().toISOString(),
      }
    },
  },
}
</script>
