<template>
    <div class="kontainer-admin">
        <div class="kontainer">
            <div class="bartipis" />
            <div class="">
                <h1 class="teks-admin">Admin desa Bahomoleo</h1>
                <p class="teks-kabupaten">Kabupaten, Morowali</p>
            </div>
        </div>
    </div>

    <div class="container">
        <div class="row">
            <div class="col">
                <h3 class="title-warga">Tambah Data Desa</h3>
                <p class="subtitle-warga">Management Content dan Layanan Warga</p>
            </div>
        </div>

        <div class="content-warga">
            <p class="header-title">Form Nama</p>
        </div>
        <div class="isi-tambahdata">
            <div class="grid-container">
                <div class="field1">
                    <div class="form-group">
                        <label for="NamaLengkap">Judul</label>
                        <input type="text" v-model="detail[0].judul " class="form-control" id="NamaLengkap"
                            aria-label="nama" disabled />
                    </div>
                </div>

                <div class="field2">
                    <div class="form-group">
                        <label for="Umur">Sub Judul</label>
                        <input type="text" v-model="detail[0].sub_judul" class="form-control" id="Umur" aria-label="umur"
                            disabled />
                    </div>
                </div>

                <div class="field3">
                    <div class="form-group">
                        <label for="NIK">Deskripsi</label>
                        <textarea type="text" v-model="detail[0].deskripsi" class="form-control" id="NIK" aria-label="nik" disabled />
                    </div>
                </div>

                <div class="field4">
                    <div class="form-group">
                        <label for="KK">Foto Berita</label>
                        <input type="text" v-model="detail[0].foto_berita" class="form-control" id="KK" aria-label="kk" disabled />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
  
<script>
import axios from "axios";
import { array } from "prop-types";

export default {
    data() {
        return {
            id: this.$route.params.id,
            detail: [],
        };
    },
    methods: {
        getDetail() {
            axios.get(`http://localhost:8080/berita/${this.id}`)
                .then(response => {
                    const data = response.data.data;
                    this.detail = data;
                    console.log(this.detail[0]);
                })
                .catch(error => {
                    console.error('Error fetching detail:', error);
                });
        },
    },
    created() {
        this.getDetail();
        console.log(this.id);
    },
};
</script>
  
<style scoped>
h3 {
    font-weight: 700;
}

.container {
    margin-top: 30px;
    margin-bottom: 50px;
    width: calc(100% - 100px);
}

.title-warga {
    font-size: 20px;
}

.subtitle-warga {
    font-size: 15px;
    color: #5e5e5e;
}

.content-warga {
    background-color: #f7f7f7;
    padding-top: 20px;
    padding-bottom: 5px;
    padding-left: 20px;
    border-radius: 3px;
    border: 1px solid #c7c7c7;
}

.header-title {
    font-weight: bold;
    color: #000000;
}

.isi-tambahdata {
    background-color: #ffffff;
    padding-top: 20px;
    padding-bottom: 5px;
    padding-left: 20px;
    border-radius: 3px;
    border: 1px solid #c7c7c7;
}

.grid-container {
    display: grid;
    grid-template-columns: auto auto auto;
    grid-gap: 40px;
    padding: 10px;
    padding-right: 30px;
}

.btn-simpan {
    background-color: #003366;
    color: #fff;
    border: none;
}

.btn-simpan:hover {
    background-color: #003366;
    color: #fff;
    border: none;
}

.teks-tambah {
    font-size: 15px;
    padding-top: 2%;
    padding-bottom: 2%;
    padding-left: 5px;
    padding-right: 5px;
}</style>
  