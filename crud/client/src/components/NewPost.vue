<template>
  <div class="posts">
    <h1>Add Post</h1>
      <div class="form">
        <div>
          <input type="text" name="title" placeholder="TITLE" v-model="title">
        </div>
        <div class="container">
          <div class="row">
            <div class="col-md-12">
                <date-picker name="date" v-model="date" :config="options" align="center"></date-picker>
            </div>
          </div>
        </div>
        <div>
          <textarea rows="15" cols="15" placeholder="Room number" v-model="description"></textarea>
        </div>
        <div>
          <button class="app_post_btn" @click="addPost">Add</button>
        </div>
      </div>
  </div>
</template>

<script>
import PostsService from '@/services/PostsService'

import 'bootstrap/dist/css/bootstrap.css'
import datePicker from 'vue-bootstrap-datetimepicker'
import 'pc-bootstrap4-datetimepicker/build/css/bootstrap-datetimepicker.css'

export default {
  name: 'NewPost',
  data () {
    return {
      title: '',
      description: '',
      date: new Date(),
      options: {
        format: 'YYYY-MM-DD',
        useCurrent: false
      }
    }
  },
  methods: {
    async addPost () {
      await PostsService.addPost({
        title: this.title,
        description: this.description,
        date: this.date
      })
      this.$router.push({ name: 'Posts' })
    }
  },
  components: {
    datePicker
  }
}
</script>

<style type="text/css">
.form input, .form textarea {
  width: 500px;
  padding: 10px;
  border: 1px solid #e0dede;
  outline: none;
  font-size: 12px;
}
.form div {
  margin: 20px;
}
.app_post_btn {
  background: #4d7ef7;
  color: #fff;
  padding: 10px 80px;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: bold;
  width: 520px;
  border: none;
  cursor: pointer;
}
</style>
