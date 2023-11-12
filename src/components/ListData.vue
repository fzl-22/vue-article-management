<template>
  <v-app>
    <v-main>
      <v-card v color="transparent"  class="d-flex justify-center text-center" >
        <v-table class="mt-5 text-center  " hover="true">
          <template v-slot:default>
            <thead>
              <tr class="bg-purple  text-center">
                <th class="text-center " style="color: white;">Judul</th>
                <th class="text-center " style="color: white;">gambar</th>
                <th class="text-center " style="color: white;">Date</th>
                <th class="text-center " style="color: white;">Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="artikel in artikels" :key="artikel.id">
                <td class="bg-pink" style="width: 50%">{{ artikel.judul }}</td>
                <td class="bg-pink"><v-img height="125" v-bind:src="artikel.image" alt="gambar" /></td>
                <td class="bg-pink">{{ artikel.date }}</td>
                <td class="bg-pink">
                  <v-btn class="bg-yellow mx-3" @click="getDatabyId(artikel.id)">
                    <v-icon color="black">mdi-pencil</v-icon>
                  </v-btn>
                  <v-btn class="bg-red-darken-1" @click="deleteData(artikel.id)">
                    <v-icon color="black">mdi-delete</v-icon>
                  </v-btn>
                </td>
              </tr>
            </tbody>
          </template>
        </v-table>
        <v-dialog v-model="dialogFormAdd" max-width="600">
          <v-card>
            <v-card-title>
              Tambah Data
            </v-card-title>
            <v-card-text>
              <v-text-field v-model="formData.id" label="ID" readonly></v-text-field>
              <v-text-field v-model="formData.judul" label="Judul"></v-text-field>
              <v-text-field v-model="formData.image" label="URL Gambar"></v-text-field>
              <v-text-field v-model="formData.date" label="Tanggal"></v-text-field>
              <v-textarea v-model="formData.content" label="Konten"></v-textarea>
            </v-card-text>
            <v-card-actions>
              <v-btn @click="addData">Simpan</v-btn>
              <v-btn @click="dialogForm = false">Batal</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogEditForm" max-width="600">
          <v-card>
            <v-card-title>
              Edit Data
            </v-card-title>
            <v-card-text>
              <v-text-field v-model="formData.id" label="ID" readonly></v-text-field>
              <v-text-field v-model="formData.judul" label="Judul"></v-text-field>
              <v-text-field v-model="formData.image" label="URL Gambar"></v-text-field>
              <v-text-field v-model="formData.date" label="Tanggal"></v-text-field>
              <v-textarea v-model="formData.content" label="Konten"></v-textarea>
            </v-card-text>
            <v-card-actions>
              <v-btn @click="updateData()">Simpan</v-btn>
              <v-btn @click="dialogEditForm = false">Batal</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-card>
      <v-btn class="mx-5 my-5" color="#e040fb" @click="formMasuk">
          <v-icon>mdi-plus</v-icon>
      </v-btn>
    </v-main>
  </v-app>
</template>
<script>
import { reactive } from 'vue';

export default {
  name: 'ListData',
  data() {
    return {
      dialogFormAdd : false,
      dialogEditForm: false,
      formData : {
        id: '',
        judul: '',
        image: '',
        date: '',
        content: '',

      },
      artikels: [
        {
          id: '1',
          judul : 'Transformasi Digital Al-Barra Studio Melalui Pembuatan Website oleh Institut Teknologi Telkom Surabaya',
          image : 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/11/transformasi-digital.jpg',
          date : '08-11-2023',
          content: 'Tranformasi Digital semakin meluas ke berbagai bidang dan menjadi merasakan dampak positif dari transformasi digital ini, berkat kolaborasi dengan Tim Pengabdian kepada Masyarakat Institut Teknologi Telkom Surabaya. Pada tanggal 01 November 2023, tim melaksanakan kunjungan ke Al-Barra Studio untuk menyerahkan situs web yang telah dibuat dan panduan penggunaannya. Kegiatan pengabdian masyarakat ini sering kali dilakukan oleh civitas akademika ITTelkom Surabaya secara rutin sebagai bagian mewujudkan Tri Dharma Perguruan Tinggi.',
        },
        {
          id: '2',
          judul : 'Kunjungan LLDIKTI 4: Selangkah lebih Dekat Menuju Telkom University National Campus (TUNC) Surabaya',
          image : 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/11/Telkom-University-National-Campus.jpg',
          date : '03-11-2023',
          content: 'Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) makin mendekatkan diri pada penyatuan dengan Telkom University, ditandai oleh kunjungan Lembaga Layanan Pendidikan Tinggi (LLDIKTI) Wilayah IV ke kampus pada 3 November 2023. Dalam sambutannya, Direktur Utama Yayasan Pendidikan Telkom, Dody Irawan, menjelaskan rencana pengembangan Telkom University National Campus (TUNC). Rektor ITTelkom Surabaya, Prof. Dr. Tri Arief Sardjono S.T. M.T., menegaskan komitmen untuk menjaga kualitas pendidikan tinggi. Diskusi antara kedua belah pihak menyoroti aspek teknis dan akademis penyatuan, dengan keyakinan bahwa bergabung dengan Telkom University membuka peluang luas. Perwakilan LLDIKTI 4, Syamsuri, menekankan kekuatan ITTelkom Surabaya sebagai tambahan signifikan, dengan penjaminan sarana dan prasarana serta standar kualitas yang dipertahankan. Kunjungan ini bukan hanya untuk memastikan kualitas pendidikan tinggi tetap terjaga, tetapi juga untuk membangun jaringan dan kerjasama yang kuat, menciptakan harapan kesuksesan penyatuan ini di masa depan.',
        },
        {
          id: '3',
          judul: 'Desa Cerdas: Kolaborasi ITTelkom Surabaya dan ADIDES yang Menerangi Masa Depan',
          image: 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/10/institut-teknologi-telkom-surabaya.jpg',
          date: '27-10-2023',
          content: 'Pada Kamis (26/10/2023), ruang rapat lantai 3 Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) menjadi panggung dari sebuah peristiwa bersejarah yang akan mengubah wajah pengembangan desa di Indonesia. Hari itu, ITTelkom Surabaya dan Asosiasi Dosen Integrator Desa (ADIDES) merayakan penandatanganan Memorandum of Understanding (MoU) yang memulai perjalanan menuju pengembangan desa yang lebih cerdas dan berkelanjutan di seluruh negeri.'
        },
        {
          id: '4',
          judul: 'Panduan Sukses Meraih Pendanaan Riset dan Inovasi BRIN: Tips dari Workshop ITTelkom Surabaya',
          image: 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/10/BRIN.jpeg',
          date: '18-10-2023',
          content: 'Lembaga Penelitian dan Pengabdian Masyarakat (LPPM) Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) menggelar workshop yang membuka rahasia sukses dalam meraih pendanaan riset dan inovasi dari BRIN. Workshop bertajuk “Sukses Meraih Pendanaan Riset dan Inovasi BRIN” ini menghadirkan pembicara ahli, Dr. Riandar, yang juga merupakan bagian dari research center for artificial intelligence and cybersecurity di BRIN. Acara ini berlangsung pada Rabu (18/10/2023) di Aula Kampus ITTelkom Surabaya.'
        },
        {
          id: '5',
          judul: 'Meningkatkan Talenta Digital di Indonesia: Peran Institut Teknologi Telkom Surabaya dalam Pelatihan Social Media Analysis',
          image: 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/10/institut-teknologi-telkom-surabaya-2-1024x576.jpeg',
          date: '18-10-2023',
          content: 'Perkembangan teknologi digital yang pesat telah mengubah lanskap cara masyarakat berinteraksi, berbagi opini, berbelanja online, dan berkomunikasi. Dampaknya sangat besar, terutama dalam hal data. Setiap hari, volume data yang dihasilkan terus meningkat dengan pesat. Data-data ini, sebagian besar bersifat publik, berasal dari media sosial, blog, berita, forum diskusi, dan sumber data publik lainnya yang dikeluarkan oleh pemerintah. Semua data ini memiliki potensi besar untuk memberikan wawasan berharga. Terutama, data yang melimpah dari media sosial menjadi aset berharga dalam memahami opini publik, tren terkini, dan aktor-aktor berpengaruh dalam penyebaran informasi di internet. Dalam berbagai bidang, pemahaman data media sosial menjadi kunci untuk pengambilan keputusan yang lebih baik dan relevan. Tantangan besar muncul ketika kita berhadapan dengan data media sosial yang tidak terstruktur dan berlimpah. Di sinilah peran penting Tim Pengabdian kepada Masyarakat Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) muncul.'
        },
        {
          id: '6',
          judul: 'Institut Teknologi Telkom Surabaya Gelar Wisuda Ke-3: 50 Lulusan Telah Bekerja',
          image: 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/10/wisuda.jpg',
          date: '16-10-2023',
          content: 'Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) menggelar Wisuda ke-3 Tahun Akademik 2022/2023 di Lapangan Tenis ITTelkom Surabaya, Sabtu (14/10/2023). Periode kali ini melibatkan 271 lulusan dari tujuh program studi yang menandai awal perjalanan mereka di dunia profesional.',
        },
        {
          id: '7',
          judul : 'Pengenalan IoT kepada Generasi Muda: Workshop di SMP Al Islah Surabaya oleh IT Telkom Surabaya',
          image : 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/10/pengenalan-IoT-1024x768.jpeg',
          date : '12-10-2023',
          content: 'ITTelkom Surabaya mengadakan workshop "Pengenalan IoT kepada Generasi Muda" di SMP Al Islah Surabaya, pada 6 September 2023, dengan tujuan memperkenalkan konsep Internet of Things (IoT) kepada siswa SMP. Workshop ini melibatkan dosen dan mahasiswa Teknik Komputer ITTelkom Surabaya, memberikan siswa pemahaman dan keterampilan teknis dalam menghadapi era teknologi yang semakin terkoneksi. Ardiansyah Al Farouq, S.ST., M.T., ketua kegiatan, menekankan pentingnya mengisi kesenjangan pemahaman IoT di kalangan siswa SMP. Kegiatan ini merupakan bagian dari komitmen ITTelkom Surabaya dalam mendukung pendidikan dan pengembangan teknologi di komunitas lokal, sekaligus merangkum Tri Dharma Perguruan Tinggi. Saat ini, institusi ini mengalami restrukturasi menjadi Telkom University dengan peningkatan di berbagai aspek, termasuk fasilitas dan kurikulum, untuk memberikan manfaat jangka panjang bagi mahasiswa dalam menghadapi masa depan yang semakin terkoneksi.',
        },
        
        {
          id: '8',
          judul : 'Tiga Mahasiswa IT Telkom Surabaya Bersinar di Konferensi Internasional ISICO 2023',
          image : 'https://10tph8qrsp2c6.cdn.shift8web.com/wp-content/uploads/2023/09/ISICO-2023.jpg',
          date : '19-09-2023',
          content: 'Tiga mahasiswa berbakat dari Program Studi Sistem Informasi Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) telah menciptakan sejarah gemilang dengan prestasi luar biasa mereka di Konferensi Internasional Sistem Informasi dan Komputer (ISICO) 2023. Konferensi yang diadakan di Hotel Prama Sanur Beach, Bali, mulai dari 26 Juli hingga 28 Juli 2023, ini telah menjadi ajang yang paling dinanti-nantikan oleh para ilmuwan dan praktisi teknologi informasi di seluruh dunia.',
        },
        
        
      ],
      }
    },
    methods : {
      formMasuk(){
        this.formData = {
          id: this.generateId(),
          judul: '',
          image: '',
          date: '',
          content: '',
        };
        this.dialogFormAdd = true;
      },
      addData(){
        if (this.formData.judul && this.formData.image && this.formData.date && this.formData.content) {
          this.artikels.push({
            id: this.formData.id,
            judul: this.formData.judul,
            image: this.formData.image,
            date: this.formData.date,
            content: this.formData.content,
          });
          this.dialogForm = false;
        } else {
          alert('ID Tidak Ditemukan');
        }
      },
      getDatabyId(id){
        const selectedArtikel = this.artikels.find((artikel) => artikel.id === id);
        if (selectedArtikel) {
        // Mengisi formulir edit dengan nilai artikel yang akan diedit
          this.formData = {
            id: selectedArtikel.id,
            judul: selectedArtikel.judul,
            image: selectedArtikel.image,
            date: selectedArtikel.date,
            content: selectedArtikel.content,
          };
          this.dialogEditForm = true;
        }
      },
      updateData(){
        if (this.formData.judul && this.formData.image && this.formData.date && this.formData.content) {
          const index = this.artikels.findIndex((artikel) => artikel.id === this.formData.id);
          if (index !== -1) {
            this.artikels[index] = reactive({...this.formData})
            this.dialogEditForm = false;
          } else {
            alert('ID tidak ditemukan');
          }
        }
      },
      deleteData(id){
        const deleteConfirm = window.confirm("Apakah anda ingin menghapus ini?");
        if (deleteConfirm) {
          this.artikels = this.artikels.filter((artikel) => artikel.id !== id);
        }
      },
      generateId(){
        return(this.artikels.length + 1).toString();
      },
    },
  }
</script>

<style>
template{
  background-image: url('https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.pixground.com%2Fcolorful-background-dynamic-waves-ai-generated-4k-wallpaper%2F&psig=AOvVaw1_BTdFdEHXKR5_5mN1b2rV&ust=1699879599336000&source=images&cd=vfe&opi=89978449&ved=0CBEQjRxqFwoTCPCJgo-_voIDFQAAAAAdAAAAABAI');
  background-size: cover;
  height: 100vh;
}
</style>
