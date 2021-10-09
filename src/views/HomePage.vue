<template>
<div class="card border p-2">
    <div class="d-flex justify-content-end">
<button class="btn btn-primary btn-sm" @click="$router.push({name: 'NewBookMark'})">Yeni Ekle</button>
</div>
    <table class="table table-striped table-hover">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Başlık</th>
      <th scope="col">URL</th>
      <th scope="col">Açıklama</th>
      <th scope="col">Sil</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="bookmark in bookmarkList" :key="bookmark">
      <th scope="row">{{bookmark.id}}</th>
      <td>{{bookmark.title}}</td>
      <td>{{bookmark.url}}</td>
      <td>{{bookmark.description}}</td>
      <td>
          <button @click="deleteBookmark(bookmark)" class="btn btn-sm btn-danger">Sil</button>
      </td>
    </tr>
   
  </tbody>
</table>
</div>
</template>

<script>
export default {
  data(){
    return{
      bookmarkList : []
    }
  },
  created(){
    this.$appAxios.get("/bookmarks").then(bookmarks_list_response => {
      this.bookmarkList = bookmarks_list_response.data 
    })
  },
  methods:{
    deleteBookmark(bookmark){
      this.$appAxios.delete(`/bookmarks/${bookmark.id}`).then(delete_response => {
        if(delete_response.status == 200){
          this.bookmarkList = this.bookmarkList.filter(b => b.id !=bookmark.id)
        }
      })

    }
  }
}
</script>