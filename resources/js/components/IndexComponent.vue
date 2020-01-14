<template>
  <div>
      <h1>Posts</h1>
        <div class="row">
          <div class="col-md-10"></div>
          <div class="col-md-2">
            <router-link :to="{ name: 'create' }" class="btn btn-primary">Create Post</router-link>
          </div>
        </div><br />
        <div class="alert alert-success" role="alert" v-if="bandera">
            Eliminado correctamente
        </div>
        <li class="list-group-item">
            <input type="text" placeholder="Buscar" class="form-control" v-model="name"  @keyup="Filtrar()">
        </li>
        <table class="table table-hover">
            <thead>
            <tr>
                <th>ID</th>
                <th>Item Name</th>
                <th>Item Price</th>
                <th>Actions</th>
            </tr>
            </thead>
            <tbody>
                <tr v-for="post in posts.data" :key="post.id">
                    <td>{{ post.id }}</td>
                    <td>{{ post.title }}</td>
                    <td>{{ post.body }}</td>
                    <td><router-link :to="{name: 'edit', params: { id: post.id }}" class="btn btn-primary">Edit</router-link></td>
                    <td><button class="btn btn-danger" @click.prevent="deletePost(post.id)">Delete</button></td>
                </tr>
            </tbody>
        </table>
        <pagination
            :data="posts"
            @pagination-change-page="getResults"></pagination>
  </div>
</template>

<script>
  export default {
      data() {
        return {
          posts: {},
          bandera:false,
          name:'',
        }
      },
      created() {
      let uri = 'http://127.0.0.1:8001/api/posts';
      this.axios.get(uri).then(response => {
        this.posts = response.data;
      });
    },
    methods: {
      deletePost(id)
      {
        let uri = `http://127.0.0.1:8001/api/post/delete/${id}`;
        this.axios.delete(uri).then(response => {
          this.posts.splice(this.posts.indexOf(id), 1);
          this.bandera=true;
        });
      },
      getResults(page = 1) {
			axios.get('http://127.0.0.1:8001/api/posts?page=' + page)
				.then(response => {
                    console.log(response.data)
					this.posts = response.data;
				});
        },
        Filtrar: function () {
                return this.posts.data.filter((item) => item.body.includes(this.name));
        }
    },
    computed: {

    }
  }
</script>
