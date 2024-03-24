<template>
  <div class="container-fluid">
    <div class="row my-5 d-flex justify-content-between">
      <div class="col-lg-5 mb-5">
        <nuxt-link to="/pengunjung/tambah" class="tbh text-decoration-none">
          <div class="card bg-pengunjung rounded-5">
            <div class="card-body d-flex justify-content-center align-items-center">
              <h2 class="text-white">Pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
      <div class="col-lg-5">
        <nuxt-link to="/buku" class="bk text-decoration-none">
          <div class="card bg-buku rounded-5">
            <div class="card-body d-flex justify-content-center align-items-center">
              <h2 class="text-white">Cari Buku</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
    <div class="row justify-content-md-center pb-5">
      <div class="col-lg-5">
        <nuxt-link to="/pengunjung" class="pjg text-decoration-none">
          <div class="card bg-riwayat rounded-5">
            <div class="card-body d-flex justify-content-center align-items-center">
              <h2 class="text-white p-10">Daftar Pengunjung</h2>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()
console.log(supabase)
</script>

<style scoped>
.card {
  height: 250px;
  box-shadow: 1px 1px 10px #424242;
}

.card.bg-pengunjung {
  background-image: url('../assets/img/bg-home-kunjungan.jpeg');
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
}

.card.bg-buku {
  background: url('../assets/img/bg-home-cari-buku.jpg') no-repeat center center;
  background-size: cover;
}

.card.bg-riwayat {
  background: url('../assets/img/riwayat.jpg') no-repeat center center;
  background-size: cover;
}
</style>