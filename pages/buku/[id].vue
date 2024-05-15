<script setup>
import { ref, onMounted } from 'vue'
const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref(null)

const getBookById = async () => {
  const { data, error } = await supabase.from('Buku').select(`*, kategori(nama)`)
    .eq('id', route.params.id)
  if (data) buku.value = data[0]
}


onMounted(async () => {
  await getBookById()
})
</script>

<template>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
  <div v-if="buku" class="container">
    <div class="row mt-3">
      <div class="col-lg-6 pt-5 d-flex justify-content-center">
        <div class="card p-0">
          <div class="card-body p-0">
            <img :src="buku.cover" width="220px" height="340px" class="cover" alt="cover1">
          </div>
        </div>
      </div>
      <div class="col-lg-6 pt-5 justify-content-center">
        <p>Judul : {{ buku.judul }}</p>
            <p>Penulis : {{ buku.penulis }}</p>
            <p>Kategori : {{ buku.kategori.nama}}</p>
            <p>Penerbit : {{ buku.penerbit }}</p>
            <p>Tahun : {{ buku.tahun_terbit }}</p>
      </div>
    </div>
    <div class="row mt-5">
      <h2>Sinopsis</h2>
      <p class="mt-3">{{ buku.deskripsi }}</p>
    </div>

    <nuxt-link to="/buku">
      <button type="button" class="btn btn-dark mt-5 mb-5">Kembali</button>
    </nuxt-link>
  </div>
</body>
</html>
</template>


<style scoped>
.cover {
  width: 255px;
  height: 370px;
  box-shadow: 1px 10px 50px rgb(0, 0, 0, .5);
}

.card {
  border: none !important;
}

.card-body {
  width: auto;
}
</style>
