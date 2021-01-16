<template>
  <div class="container column">
    <app-form @addTitleOrAvatar="addTitleOrAvatar" @addDescription="addDescription"></app-form>

    <div class="card card-w70">
      <app-title :title="title"></app-title>
      <app-avatar :src="avatar"></app-avatar>
      <app-description :description="description"></app-description>

      <h3 v-if="isEmpty">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>

  <div class="container">
    <p>
      <button class="btn primary" @click="comments.length ? clearComments() : loadComments()">
        {{ comments.length ? 'Скрыть' : 'Загрузить' }} комментарии
      </button>
    </p>

    <app-comment-list :comments="comments" :loading="loading"></app-comment-list>
  </div>
</template>

<script>
import AppForm from './components/AppForm'
import AppTitle from './components/AppTitle'
import AppAvatar from './components/AppAvatar'
import AppDescription from './components/AppDescription'
import AppCommentList from './components/AppCommentList'

import axios from 'axios'

export default {
  data () {
    return {
      title: '',
      avatar: '',
      description: [],
      comments: [],
      loading: false
    }
  },
  methods: {
    addTitleOrAvatar (type, text) {
      this[type] = text
    },
    addDescription (type, text) {
      this.description.push({ id: Math.random(), type, text })
    },
    async loadComments () {
      this.loading = true
      const response = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
      setTimeout(() => {
        this.loading = false
        this.comments = response.data
      }, 1000)
    },
    clearComments () {
      this.comments = []
    }
  },
  computed: {
    isEmpty () {
      return !this.title && !this.avatar && !this.description.length
    }
  },
  components: {
    AppForm, AppTitle, AppAvatar, AppDescription, AppCommentList
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
