<template>
  <div>
    <div class="px-4 text-center mx-auto">
      <h1 class="font-bold text-lg mb-4">NIK Parser</h1>
      <input placeholder="Masukkan NIK" type="number" class="px-4 h-10 block w-full border rounded-md" v-model="nik">
    </div>
    <div class="grid grid-cols-2 mt-8 gap-4 px-4">
      <div>Tanggal Lahir</div>
      <div>{{tl}}</div>
    </div>
    <div class="grid grid-cols-2 mt-4 gap-4 px-4">
      <div>Provinsi</div>
      <div>{{prov}}</div>
    </div>
    <div class="grid grid-cols-2 mt-4 gap-4 px-4">
      <div>Kabupaten / Kota</div>
      <div>{{kab}}</div>
    </div>
    <div class="grid grid-cols-2 mt-4 gap-4 px-4">
      <div>Kecamatan</div>
      <div>{{kec}}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: [],
      nik: 'Masukkan NIK',
      prov: '',
      kab: '',
      kec: '',
      tl: ''
    }
  },
  mounted() {
    this.$axios.get('/wilayah.json').then(r=> {
      this.data = r.data
    })
  },
  watch: {
    nik: {
      handler(r) {
        var prov = this.data.provinsi[r.slice(0,2)]
        var kab = this.data.kabkot[r.slice(0,4)]
        var kec = this.data.kecamatan[r.slice(0,6)]
        var tl = r.slice(6,12)
        this.prov = prov
        this.kab = kab
        this.kec = kec
        this.tl = tl        
      }
    }
  }
}
</script>