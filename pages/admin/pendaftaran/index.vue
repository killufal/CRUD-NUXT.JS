<template>

  <div class="content-wrapper mb-5">
    <section class="content-header">
      <div class="container-fluid">
      </div>
    </section>

    <section class="content">
      <div class="card card-outline card-info">
        <div class="card-header">
          <h3 class="card-title"><i class="nav-icon fas fa-folder"></i> Data Pendaftaran</h3>
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
          <div class="form-group">
            <div class="input-group mb-3">
              <div class="input-group-prepend">
                <nuxt-link :to="{ name: 'admin-pendaftaran-create' }" class="btn btn-info btn-sm"
                  style="padding-top: 8px;">
                  <i class="fa fa-plus-circle"></i> Tambah
                </nuxt-link>
              </div>
              <input type="text" class="form-control" v-model="search" @keypress.enter="searchData"
                placeholder="Search">
              <div class="input-group-append">
                <button @click="searchData" class="btn btn-info"><i class="fa fa-search"></i>
                  Find
                </button>
              </div>
            </div>
          </div>

          <!-- table -->
          <b-table striped bordered hover :items="pendaftarans" :fields="fields" show-empty>
            <template v-slot:cell(image)="data">
              <img class="img-fluid" width="50" :src="data.item.image" />
            </template>
            <template v-slot:cell(actions)="row">
              <b-button :to="{ name: 'admin-pendaftaran-edit-id', params: { id: row.item.id } }" variant="warning"
                size="sm">
                Edit
              </b-button>
              <b-button variant="danger" size="sm" @click="deletePendaftaran(row.item.id)">Hapus</b-button>
            </template>
          </b-table>

          <!-- pagination -->

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

  //data function
  data() {
    return {

      //table header
      fields: [{
        label: 'Nomor Pendaftaran',
        key: 'nomor',
      },
      {
        label: 'Nama',
        key: 'nama'
      },
      {
        label: 'Kompetensi',
        key: 'kompetensi'
      },
      {
        label: 'Hobby',
        key: 'hobby'
      },
      {
        label: 'Profil',
        key: 'profil'
      },
      {
        label: 'Actions',
        key: 'actions',
      }
      ],

      //state search
      search: ''
    }
  },

  //watch query URL
  
  watchQuery: ["q", "page"],

  async asyncData({ $axios, query }) {

    //page
    let page = query.page ? parseInt(query.page) : ''

    //search
    let search = query.q ? query.q : ''

    //fetching pendaftarans
    const pendaftarans = await $axios.$get(`/api/admin/pendaftarans?q=${search}&page=${page}`)

    return {
      'pendaftarans': pendaftarans.data.data,
    }
  },

  methods: {

    //change page pagination
    changePage(page) {
      this.$router.push({
        path: this.$route.path,
        query: {
          q: this.$route.query.q,
          page: page
        }
      });
    },

    //searchData
    searchData() {
      this.$router.push({
        path: this.$route.path,
        query: {
          q: this.search
        }
      });
    },


    //deletePendaftaran method
    deletePendaftaran(id) {
      this.$swal.fire({
        title: 'APAKAH ANDA YAKIN ?',
        text: "INGIN MENGHAPUS DATA INI !",
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#d33',
        cancelButtonColor: '#3085d6',
        confirmButtonText: 'YA, HAPUS!',
        cancelButtonText: 'TIDAK',
      }).then((result) => {
        if (result.isConfirmed) {

          //delete tag from server
          this.$axios.delete(`/api/admin/pendaftarans/${id}`)
            .then(() => {

              //feresh data
              this.$nuxt.refresh()

              //alert
              this.$swal.fire({
                title: 'BERHASIL!',
                text: "Data Berhasil Dihapus!",
                icon: 'success',
                showConfirmButton: false,
                timer: 2000
              })

            })
        }
      })
    } 

  }

}
</script>

<style>
</style>
