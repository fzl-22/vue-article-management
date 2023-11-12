<template>
    <v-app>
      <v-main>
        <v-card v color="transparent"  class="d-flex justify-center text-center">
          <v-btn class="mx-2"  color="#e040fb" @click="formMasuk">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
  
          <v-table class="mt-5 text-center  " hover="true">
            <template v-slot:default>
              <thead>
                <tr class="bg-purple  text-center">
                  <th class="white--text text-center ">judul</th>
                  <th class="white--text text-center ">gambar</th>
                  <th class="white--text text-center w-50">deskripsi</th>
                  <th class="white--text text-center ">kendali</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="artikel in artikels" :key="artikel.id">
                  <td class="bg-pink">{{ artikel.judul }}</td>
                  <td class="bg-pink"><v-img height="125" v-bind:src="artikel.image" alt="gambar" /></td>
                  <td class="bg-pink">{{ artikel.content }}</td>
                  <td class="bg-pink">
                    <v-btn>
                      <v-icon color="black">mdi-pencil</v-icon>
                    </v-btn>
                    <v-btn>
                      <v-icon color="black">mdi-delete</v-icon>
                    </v-btn>
                  </td>
                </tr>
              </tbody>
            </template>
          </v-table>
        </v-card>
      </v-main>
    </v-app>
  </template>
  
  <script>
  export default {
    name: 'ListData',
    data() {
      return {
        artikels: [
          {
            id: '1',
            judul: 'halo del',
            image: 'https://static.wikia.nocookie.net/roshidere/images/b/bf/Alisa_Mikhailovna_Kujo_Bio.png',
            content: '"Pada Kamis (26/10/2023), ruang rapat lantai 3 Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) menjadi panggung dari sebuah peristiwa bersejarah yang akan mengubah wajah pengembangan desa di Indonesia. Hari itu, ITTelkom Surabaya dan Asosiasi Dosen Integrator Desa (ADIDES) merayakan penandatanganan Memorandum of Understanding (MoU) yang memulai perjalanan menuju pengembangan desa yang lebih cerdas dan berkelanjutan di seluruh negeri."'
          },
          {
            id: '2',
            judul: 'halo mas',
            image: 'https://static.wikia.nocookie.net/roshidere/images/b/bf/Alisa_Mikhailovna_Kujo_Bio.png',
            content: '"Pada Kamis (26/10/2023), ruang rapat lantai 3 Institut Teknologi Telkom Surabaya (ITTelkom Surabaya) menjadi panggung dari sebuah peristiwa bersejarah yang akan mengubah wajah pengembangan desa di Indonesia. Hari itu, ITTelkom Surabaya dan Asosiasi Dosen Integrator Desa (ADIDES) merayakan penandatanganan Memorandum of Understanding (MoU) yang memulai perjalanan menuju pengembangan desa yang lebih cerdas dan berkelanjutan di seluruh negeri."'
          },
        ],
       
        }
      },
    }
    
  </script>
  