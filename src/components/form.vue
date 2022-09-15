<template>
  <form ref="formDaftar" @submit.prevent="handleSubmit">
    <div class="row">
      <div class="col-12 form-group">
        <label class="col-form-label">Nama <span class="text-danger">*</span></label>
        <input type="text" class="form-control" required v-model="form.nama" />
        <span v-if="form.errors().has('nama')" class="error"><small>{{ form.errors().get('nama') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">NIK <span class="text-danger">*</span></label>
        <input type="number" class="form-control" required v-model="form.nik" />
        <span v-if="form.errors().has('nik')" class="error"><small>{{ form.errors().get('nik') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Nomor Kartu Keluarga <span class="text-danger">*</span></label>
        <input type="number" class="form-control" required v-model="form.kk" />
        <span v-if="form.errors().has('kk')" class="error"><small>{{ form.errors().get('kk') }}</small></span>
      </div>
      <div class="col-12 form-group mt-2">
        <label for="formFile" class="form-label">Foto KTP <span class="text-danger">*</span></label>
        <img class="imagePreviewWrapper" :src="form.prefktp" v-if="form.prefktp" width="200" />
        <input class="form-control" type="file" v-on:change="uploadKtp" />
        <span v-if="form.errors().has('fktp')" class="error"><small>{{ form.errors().get('fktp') }}</small></span>
      </div>
      <div class="col-12 form-group mt-2">
        <label for="formFile" class="form-label">Foto Kartu Keluarga <span class="text-danger">*</span></label>
        <img class="imagePreviewWrapper" :src="form.prefkk" v-if="form.prefkk" width="200" />
        <input class="form-control" type="file" v-on:change="uploadKK" />
        <span v-if="form.errors().has('fkk')" class="error"><small>{{ form.errors().get('fkk') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Umur <span class="text-danger">*</span></label>
        <input type="number" class="form-control" required v-model="form.umur" />
        <span v-if="form.errors().has('umur')" class="error"><small>{{ form.errors().get('umur') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Jenis Kelamin <span class="text-danger">*</span></label>
        <select class="form-control" required v-model="form.jk">
          <option value="" disabled>Pilih Jenis Kelamin</option>
          <option value="Laki-laki">Laki-laki</option>
          <option value="Perempuan">Perempuan</option>
        </select>
        <span v-if="form.errors().has('jk')" class="error"><small>{{ form.errors().get('jk') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Provinsi <span class="text-danger">*</span></label>
        <select class="form-control" required v-model="form.provinsi">
          <option value="" disabled>Pilih Provinsi</option>
          <input type="text" class="form-control" required v-model="form.provinsi" />
        </select>
        <span v-if="form.errors().has('provinsi')" class="error"><small>{{ form.errors().get('provinsi') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Kab/Kota <span class="text-danger">*</span></label>
        <input type="text" class="form-control" required v-model="form.kab" />
        <span v-if="form.errors().has('kab')" class="error"><small>{{ form.errors().get('kab') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Kecamatan <span class="text-danger">*</span></label>
        <input type="text" class="form-control" required v-model="form.kec" />
        <span v-if="form.errors().has('kec')" class="error"><small>{{ form.errors().get('kec') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Kelurahan/Desa <span class="text-danger">*</span></label>
        <input type="text" class="form-control" required v-model="form.kel" />
        <span v-if="form.errors().has('kel')" class="error"><small>{{ form.errors().get('kel') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Alamat <span class="text-danger">*</span></label>
        <input type="text" class="form-control" required v-model="form.alamat" />
        <span v-if="form.errors().has('alamat')" class="error"><small>{{ form.errors().get('alamat') }}</small></span>
      </div>
      <div class="col-6 form-group">
        <label class="col-form-label">RT <span class="text-danger">*</span></label>
        <input type="number" class="form-control" required v-model="form.rt" />
        <span v-if="form.errors().has('rt')" class="error"><small>{{ form.errors().get('rt') }}</small></span>
      </div>
      <div class="col-6 form-group">
        <label class="col-form-label">RW <span class="text-danger">*</span></label>
        <input type="number" class="form-control" required v-model="form.rw" />
        <span v-if="form.errors().has('rw')" class="error"><small>{{ form.errors().get('rw') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Penghasilan sebelum pandemi <span class="text-danger">*</span></label>
        <input type="number" class="form-control" required v-model="form.penghasilan_sebelum" />
        <span v-if="form.errors().has('penghasilan_sebelum')" class="error"><small>{{
        form.errors().get('penghasilan_sebelum') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Penghasilan setelah pandemi <span class="text-danger">*</span></label>
        <input type="number" class="form-control" required v-model="form.penghasilan_sesudah"/>
        <span v-if="form.errors().has('penghasilan_sesudah')" class="error"><small>{{
        form.errors().get('penghasilan_sesudah') }}</small></span>
      </div>
      <div class="col-12 form-group">
        <label class="col-form-label">Alasan membutuhkan bantuan <span class="text-danger">*</span></label>
        <select class="form-control" required v-model="form.alasan">
          <option value="" disabled>Pilih Alasan</option>
          <option value="Kehilangan pekerjaan">Kehilangan pekerjaan</option>
          <option value="Kepala keluarga terdampak atau korban Covid-19">Kepala keluarga terdampak atau korban Covid-19
          </option>
          <option value="Tergolong fakir/miskin semenjak sebelum Covid-19">Tergolong fakir/miskin semenjak sebelum
            Covid-19</option>
          <option value="Lainnya">Lainnya</option>
        </select>
        <span v-if="form.errors().has('alasan')" class="error"><small>{{ form.errors().get('alasan') }}</small></span>
      </div>
      <div class="col-12 form-group mt-3">
        <div class="form-check">
          <input class="form-check-input" type="checkbox" required v-model="form.pernyataan" id="flexCheckDefault">
          <label class="form-check-label" for="flexCheckDefault">
            Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan
            ketidaksesuaian dalam data tersebut.
          </label>
        </div>
      </div>
      <div class="col-12 form-group text-center">
        <button class="btn btn-vue btn-lg col-4 mt-5" @click="submit">Daftar</button>
      </div>
    </div>
  </form>
</template>

<script>
import form from 'vuejs-form';

export default {
  name: "form",
  data: () => ({
    form: form({
      nama: '',
      nik: '',
      kk: '',
      fktp: '',
      fkk: '',
      umur: '',
      jk: '',
      provinsi: '',
      kab: '',
      kec: '',
      kel: '',
      alamat: '',
      rt: '',
      rw: '',
      penghasilan_sebelum: '',
      penghasilan_sesudah: '',
      alasan: '',
      pernyataan: false,
      data_provinsi: null,
      prefktp: '',
      prefkk: ''
    })
      .rules({
        nama: 'required',
        nik: 'required',
        kk: 'required',
        fktp: 'required',
        fkk: 'required',
        umur: 'required',
        jk: 'required',
        provinsi: 'required',
        kab: 'required',
        kec: 'required',
        kel: 'required',
        alamat: 'required',
        rt: 'required',
        rw: 'required',
        penghasilan_sebelum: 'required',
        penghasilan_sesudah: 'required',
        alasan: 'required',
      })
      .messages({
        'nama.required': 'Nama harus diisi',
        'nik.required': 'NIK harus diisi',
        'kk.required': 'No. KK harus diisi',
        'fktp.required': 'Foto KTP harus diupload maks 2 MB dengan format JPG/JPEG/PNG/BMP',
        'fkk.required': 'Foto KK harus diupload maks 2 MB dengan format JPG/JPEG/PNG/BMP',
        'umur.required': 'Umur harus diisi minimal 25 tahun',
        'jk.required': 'Jenis kelamin harus diisi',
        'provinsi.required': 'Provinsi harus diisi',
        'kab.required': 'Kabupaten harus diisi',
        'kec.required': 'Kecamatan harus diisi',
        'kel.required': 'Kelurahan harus diisi',
        'alamat.required': 'Alamat harus diisi',
        'rt.required': 'RT harus diisi',
        'rw.required': 'RW harus diisi',
        'penghasilan_sebelum.required': 'Penghasilan harus diisi',
        'penghasilan_sesudah.required': 'Penghasilan harus diisi',
        'alasan.required': 'Alasan harus diisi',
      }),
  }),

  methods: {
    uploadKtp(event) {
      console.log(event.target.files[0])
      var re = /(\.jpg|\.jpeg|\.png|\.bmp)$/i
      if (event.target.files[0].size < 2097152 && re.exec(event.target.files[0].name)) {
        const fotoktp = event.target.files[0].name
        this.form.fktp = fotoktp
        this.form.prefktp = URL.createObjectURL(event.target.files[0])
      }
      else {
        alert('Ukuran foto KTP maks 2 MB dengan format JPG/JPEG/PNG/BMP');
      }
    },
    uploadKK(event) {
      var re = /(\.jpg|\.jpeg|\.png|\.bmp)$/i
      if (event.target.files[0].size < 2097152 && re.exec(event.target.files[0].name)) {
        const fotokk = event.target.files[0].name
        this.form.fkk = fotokk
        this.form.prefkk = URL.createObjectURL(event.target.files[0])
      }
      else {
        alert('Ukuran foto KTP maks 2 MB dengan format JPG/JPEG/PNG/BMP');
      }
    }
    ,
    submit() {
      if (this.form.validate().errors().any()) return;
      if (this.form.umur < 25) {
        alert('Umur harus diisi minimal 25 tahun');
      }
      else {
        this.$swal({
          title: 'Data Preview',
          html: `<table>
                    <tr>
                      <td>Nama</td>
                      <td>: ${this.form.nama}</td>
                    </tr>
                    <tr>
                      <td>NIK</td>
                      <td>: ${this.form.nik}</td>
                    </tr>
                    <tr>
                      <td>Nomor KK</td>
                      <td>: ${this.form.kk}</td>
                    </tr>
                    <tr>
                      <td>Foto KTP</td>
                      <td>: ${this.form.fktp}</td>
                    </tr>
                    <tr>
                      <td>Foto KK</td>
                      <td>: ${this.form.fkk}</td>
                    </tr>
                    <tr>
                      <td>Umur</td>
                      <td>: ${this.form.umur} tahun</td>
                    </tr>
                    <tr>
                      <td>Jenis Kelamin</td>
                      <td>: ${this.form.jk}</td>
                    </tr>
                    <tr>
                      <td>Provinsi</td>
                      <td>: ${this.form.provinsi}</td>
                    </tr>
                    <tr>
                      <td>Kab/Kota</td>
                      <td>: ${this.form.kab}</td>
                    </tr>
                    <tr>
                      <td>Kecamatan</td>
                      <td>: ${this.form.kec}</td>
                    </tr>
                    <tr>
                      <td>Kelurahan/Desa</td>
                      <td>: ${this.form.kel}</td>
                    </tr>
                    <tr>
                      <td>Alamat</td>
                      <td>: ${this.form.alamat}</td>
                    </tr>
                    <tr>
                      <td>RT/RW</td>
                      <td>: ${this.form.rt} / ${this.form.rw}</td>
                    </tr>
                    <tr>
                      <td>Penghasilan Sebelum Pandemi</td>
                      <td>: Rp${this.form.penghasilan_sebelum}</td>
                    </tr>
                    <tr>
                      <td>Penghasilan Setelah Pandemi</td>
                      <td>: Rp${this.form.penghasilan_sesudah}</td>
                    </tr>
                    <tr>
                      <td>Alasan Membutuhkan Bantuan: </td>
                      <td>: ${this.form.alasan}</td>
                    </tr>
                  </table>`,
          showCancelButton: true,
          confirmButtonColor: '#3085d6',
          cancelButtonColor: '#d33',
          confirmButtonText: 'Daftar',
        }).then((result) => {
          if (result.isConfirmed) {
            this.$swal({
              title: 'Uploading',
              allowOutsideClick: false,
              timerProgressBar: true,
              timer: 1500,
              onOpen: () => {
                this.$swal.showLoading();
              },
              showConfirmButton: false,
            }).then((result) => {
              if (result.dismiss === this.$swal.DismissReason.timer) {
                this.$swal(
                  'Berhasil!',
                  `Data ${this.form.nama} berhasil didaftarkan!`,
                  'success',
                )
                this.$refs.formDaftar.reset();
              }
            })
          }
        })
      }
    }
  }
};
</script>

<style>
.btn-vue {
  background: #53b985;
  color: #31485d;
  font-weight: bold;
}

.error {
  color: red;
  margin-top: 8px;
  font-size: 0.5 rem;
}

.imagePreviewWrapper {
  width: 200px;
  max-height: 300px;
  display: block;
  cursor: pointer;
  margin: 0 auto 20px;
  background-size: cover;
  background-position: center center;
}

table {
  width: 90%;
  margin-left: auto;
  margin-right: auto;
}

td {
  width: 50%;
  text-align: left;
  height: 35px;
}
</style>