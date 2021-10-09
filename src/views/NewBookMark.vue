<template>
    <div class="form-area card border p-2">
        <div class="mb-3">
  <label for="exampleFormControlInput1" class="form-label"> Başlık</label>
  <input type="text" v-model="userData.title" class="form-control" id="title" placeholder="Başlık Alanı">
</div>
<div class="mb-3">
  <label for="exampleFormControlTextarea1" class="form-label">URL</label>
  <input class="form-control" v-model="userData.url" placeholder="https://.." id="url">
</div>
<div class="mb-3">
  <label for="exampleFormControlTextarea1" class="form-label">Açıklama</label>
  <input class="form-control"   v-model="userData.description" placeholder="Açıklama" id="description">
</div>
<div class="d-flex justify-content-end align-items-center">
    <button class="btn btn-sm btn-secondary me-1" @click="$router.push({name:'HomePage'})">İptal</button>
<button class="btn btn-sm btn-primary" @click="onSave">Kaydet</button>
</div>
    </div>
</template>

<script>
export default {
    data(){
        return{
        userData : {
            title : null,
            url : null,
            description : null
        }
    }
    },
    methods:{
        onSave(){
            this.$appAxios.post("/bookmarks",this.userData).then(save_response =>{
                this.resetData();
                this.$router.push("/");
                console.log(save_response);
            });
        },
        resetData(){
            Object.keys(this.userData).forEach(key => (this.userData[key] = null))
        }
    }
}
</script>