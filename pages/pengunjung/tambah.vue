<template>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body> 
  <nuxt-link to="/" class="bi bi-arrow-left">
  </nuxt-link>
  <div class="container">
    <div class="row d-flex justify-content-center ">
      <div class="col-lg-8">
        <h2 class="text-center my-4">ISI BUKU KUNJUNGAN</h2>
        <form @submit.prevent="kirimData">
          <div class="mb-3">
            <input v-model="form.nama" type="text" class="form-control form-control-lg rounded-3 bg-primary"
              placeholder="NAMA">
          </div>
          <div class="mb-3">
            <select v-model="form.keanggotaan" class="form-control form-control-lg form-select rounded-3 bg-primary">
              <option value="">KEANGGOTAAN</option>
              <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
            </select>
          </div>
          <div class="mb-3" v-if="form.keanggotaan === 1">
            <div class="row">
              <div class="col-md-4">
                <select v-model="form.tingkat"
                  class="form-control form-control-lg form-select rounded-3 mb-2 bg-primary">
                  <option value="">TINGKAT</option>
                  <option value="X">X</option>
                  <option value="XI">XI</option>
                  <option value="XII">XII</option>
                </select>
              </div>
              <div class="col-md-4">
                <select v-model="form.jurusan"
                  class="form-control form-control-lg form-select rounded-3 mb-2 bg-primary">
                  <option value="">JURUSAN</option>
                  <option value="PPLG">PPLG</option>
                  <option value="TJKT">TJKT</option>
                  <option value="TSM">TSM</option>
                  <option value="DKV">DKV</option>
                  <option value="TOI">TOI</option>
                </select>
              </div>
              <div class="col-md-4">
                <select v-model="form.kelas" class="form-control form-control-lg form-select rounded-3 mb-2 bg-primary">
                  <option value="">KELAS</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
          </div>
          <div class="mb-3">
            <select v-model="form.keperluan" class="form-control form-control-lg form-select rounded-3 bg-primary">
              <option value="">KEPERLUAN</option>
              <option v-for="(item, i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
            </select>
          </div>
          <div class="d-flex justify-content-center">
            <button type="submit" class="btn btn-secondary btn-lg rounded-3 px-5 text-white krm">Kirim</button>
          </div>
        </form>
      </div>
    </div>
    <nuxt-link to="/">
      <button type="button" class="btn btn-dark bck mt-5 mb-5">Kembali</button>
    </nuxt-link>
  </div>
</body>
</html>
</template>

<style scoped>
.bck {
  width: 100px;
}

.bg-primary {
  background-color: #D9D9D9 !important;
}
</style>


<script setup>
const supabase = useSupabaseClient()

const members = ref([])
const objectives = ref([])

const form = ref({
  nama: "",
  keanggotaan: "",
  tingkat: "",
  kelas: "",
  jurusan: "",
  keperluan: "",
})

const kirimData = async () => {
  // console.log(form.value)
  const { error } = await supabase.from('pengunjung').insert([form.value])
  if (!error) navigateTo('/pengunjung')
}

const getKeanggotaan = async () => {
  const { data, error } = await supabase.from('keanggotaan').select('*')
  if (data) members.value = data

}

const getKeperluan = async () => {
  const { data, error } = await supabase.from('keperluan').select('*')
  if (data) objectives.value = data
}

onMounted(() => {
  getKeanggotaan()
  getKeperluan()
})

</script>