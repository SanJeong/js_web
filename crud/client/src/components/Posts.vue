<template>
  <div class="posts">
    <h1>Selected Date: {{ day }}</h1>
    <date-pick v-model="day" :hasInputElement="false"></date-pick>
    <h1>Rooms</h1>
    <div v-if="posts.length > 0" class="table-wrap">
      <div>
        <router-link v-bind:to="{ name: 'NewPost' }" class="">Make Reservation</router-link>
      </div>

      <table>
        <tr>
          <td>Room number</td>
          <td width="450">Reserved room</td>
          <td width="200">Date</td>
          <td width="100" align="center">Action</td>
        </tr>
          <tr v-for="post in posts" :key="post.id">
            <td v-if="post.date === day">{{ post.title }}</td>
            <td v-if="post.date === day">{{ post.description }}</td>
            <td v-if="post.date === day">{{ post.date }}</td>
            <td v-if="post.date === day" align="center">
              <router-link v-bind:to="{ name: 'EditPost', params: { id: post._id } }">Edit</router-link>
              <a href="#" @click="deletePost(post._id)">Delete</a>
            </td>
          </tr>
      </table>
    </div>
    <div v-else>
      There are no reservations <br /><br />
      <router-link v-bind:to="{ name: 'NewPost' }" class="add_post_link">Add Reservation</router-link>
    </div>
  </div>

</template>

<script>
import PostsService from '@/services/PostsService'
import DatePick from 'vue-date-pick'
import 'vue-date-pick/dist/vueDatePick.css'

export default {
  name: 'posts',
  data () {
    return {
      posts: [],
      day: '2018-12-26'
    }
  },
  mounted () {
    this.getPosts()
  },
  methods: {
    async getPosts () {
      const response = await PostsService.fetchPosts()
      this.posts = response.data.posts
    },
    async deletePost (id) {
      await PostsService.deletePost(id)
      this.$router.push({ name: 'Posts' })
    }
  },
  components: {
    DatePick
  }
}
</script>

<style type="text/css">
.table-wrap {
  width: 60%;
  margin: 0 auto;
  text-align: center;
}
table th, table tr {
  text-align: left;
}
table thead {
  background: #f2f2f2;
}
table tr td {
  padding: 15px;
}
table tr:nth-child(odd) {
  background: #f2f2f2;
}
table tr:nth-child(1) {
  background: #4d7ef7;
  color: #fff;
}
a {
  color: #4d7ef7;
  text-decoration: none;
}
a.add_post_link {
  background: #4d7ef7;
  color: #fff;
  padding: 10px 80px;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: bold;
}
</style>
