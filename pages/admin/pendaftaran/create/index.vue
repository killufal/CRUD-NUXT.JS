<template>
  <div class="content-wrapper">
    <section class="content-header">
      <div class="container-fluid">
      </div>
    </section>

    <section class="content">
      <div class="card card-outline card-info">
        <div class="card-header">
          <h3 class="card-title"><i class="nav-icon fas fa-folder"></i> Tambah Data</h3>
          <div class="card-tools">
            <button type="button" class="btn btn-tool" data-card-widget="collapse" title="Collapse">
              <i class="fas fa-minus"></i>
            </button>
            <button type="button" class="btn btn-tool" data-card-widget="remove" title="Remove">
              <i class="fas fa-times"></i>
            </button>
          </div>
        </div>
        <div class="card-body">
          <form @submit.prevent="storePendaftaran">

            <div class="form-group">
              <label>Nomor Identitas</label>
              <input type="text" v-model="pendaftaran.nomor" placeholder="Nomor Identitas" class="form-control">
              <div v-if="validation.nomor" class="mt-2">
                <b-alert show variant="danger">{{ validation.nomor[0] }}</b-alert>
              </div>
            </div>

            <div class="form-group">
              <label>Nama</label>
              <input type="text" v-model="pendaftaran.nama" placeholder="Nama" class="form-control">
              <div v-if="validation.nama" class="mt-2">
                <b-alert show variant="danger">{{ validation.nama[0] }}</b-alert>
              </div>
            </div>


            <div class="form-group">
              <label>Kompetensi</label>
              <select v-model="pendaftaran.kompetensi" class="form-control">
                <option value="TAV">TAV</option>
                <option value="TEI">TEI</option>
                <option value="TSM">TSM</option>
                <option value="TKJ">TKJ</option>
                </select>
              <div v-if="validation.kompetensi" class="mt-2">
                <b-alert show variant="danger">{{ validation.kompetensi[0] }}</b-alert>
              </div>
            </div>

            <div class="form-group">
              <label>Hobby</label>
              <select v-model="pendaftaran.hobby" class="form-control">
                <option value="Internet">Internet</option>
                <option value="Memasak">Memasak</option>
                <option value="Memancing=">Memancing</option>
                </select>
              <div v-if="validation.hobby" class="mt-2">
                <b-alert show variant="danger">{{ validation.hobby[0] }}</b-alert>
              </div>
            </div>

            <div class="form-group">
              <label>Profil</label>
              <input type="text" v-model="pendaftaran.profil" placeholder="" class="form-control">
              <div v-if="validation.profil" class="mt-2">
                <b-alert show variant="danger">{{ validation.profil[0] }}</b-alert>
              </div>
            </div>

            <button class="btn btn-info mr-1 btn-submit" type="submit"><i class="fa fa-paper-plane"></i>
              Simpan</button>
            <button class="btn btn-warning btn-reset" type="reset"><i class="fa fa-redo"></i>
              Reset</button>

          </form>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  //layout
  layout: 'admin',

  //meta
  head() {
    return {
      title: '',
    }
  },

  data() {
    return {
      //state category
      pendaftaran: {
        nomor: '',
        nama: '',
        kompetensi: '',
        hobby: '',
        profil: ''
      },
      //state validation
      validation: []
    }
  },

  methods: {

    //storeCategory method
    async storePendaftaran() {

      //define formData
      let formData = new FormData();

      formData.append('nomor', this.pendaftaran.nomor)
      formData.append('nama', this.pendaftaran.nama)
      formData.append('kompetensi', this.pendaftaran.kompetensi)
      formData.append('hobby', this.pendaftaran.hobby)
      formData.append('profil', this.pendaftaran.profil)

      //sending data to server
      await this.$axios.post('/api/admin/pendaftarans', formData)
        .then(() => {

          //sweet alert
          this.$swal.fire({
            title: 'BERHASIL!',
            text: "Data Berhasil Disimpan!",
            icon: 'success',
            showConfirmButton: false,
            timer: 2000
          })

          //redirect, if success store data
          this.$router.push({
            name: 'admin-pendaftaran'
          })

        })
        .catch(error => {

          //assign error to state "validation"
          this.validation = error.response.data
        })
    }
  }

}
</script>

<style>
</style>
