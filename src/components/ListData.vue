<template>
  <v-app>
    <v-main>
      <v-card v color="transparent" class="d-flex justify-center text-center">
        <v-table class="mt-5 text-center" hover="true">
          <template v-slot:default>
            <thead>
              <tr class="bg-purple text-center">
                <th class="text-center" style="color: white">Judul</th>
                <th class="text-center" style="color: white">gambar</th>
                <th class="text-center" style="color: white">Date</th>
                <th class="text-center" style="color: white">Action</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="artikel in artikels" :key="artikel.id">
                <td class="bg-pink" style="width: 50%">{{ artikel.judul }}</td>
                <td class="bg-pink">
                  <v-img height="125" v-bind:src="artikel.image" alt="gambar" />
                </td>
                <td class="bg-pink">{{ artikel.date }}</td>
                <td class="bg-pink">
                  <v-btn
                    class="bg-yellow mx-3"
                    @click="getDatabyId(artikel.id)"
                  >
                    <v-icon color="black">mdi-pencil</v-icon>
                  </v-btn>
                  <v-btn
                    class="bg-red-darken-1"
                    @click="deleteData(artikel.id)"
                  >
                    <v-icon color="black">mdi-delete</v-icon>
                  </v-btn>
                </td>
              </tr>
            </tbody>
          </template>
        </v-table>
        <v-dialog v-model="dialogFormAdd" max-width="600">
          <v-card>
            <v-card-title> Tambah Data </v-card-title>
            <v-card-text>
              <v-text-field
                v-model="formData.id"
                label="ID"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="formData.judul"
                label="Judul"
              ></v-text-field>
              <v-text-field
                v-model="formData.image"
                label="URL Gambar"
              ></v-text-field>
              <v-text-field
                v-model="formData.date"
                label="Tanggal"
              ></v-text-field>
              <v-textarea
                v-model="formData.content"
                label="Konten"
              ></v-textarea>
            </v-card-text>
            <v-card-actions>
              <v-btn @click="addData">Simpan</v-btn>
              <v-btn @click="dialogForm = false">Batal</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-dialog v-model="dialogEditForm" max-width="600">
          <v-card>
            <v-card-title> Edit Data </v-card-title>
            <v-card-text>
              <v-text-field
                v-model="formData.id"
                label="ID"
                readonly
              ></v-text-field>
              <v-text-field
                v-model="formData.judul"
                label="Judul"
              ></v-text-field>
              <v-text-field
                v-model="formData.image"
                label="URL Gambar"
              ></v-text-field>
              <v-text-field
                v-model="formData.date"
                label="Tanggal"
              ></v-text-field>
              <v-textarea
                v-model="formData.content"
                label="Konten"
              ></v-textarea>
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
import { reactive } from "vue";
import articles from "../data/articles";

export default {
  name: "ListData",
  data() {
    return {
      dialogFormAdd: false,
      dialogEditForm: false,
      formData: {
        id: "",
        judul: "",
        image: "",
        date: "",
        content: "",
      },
      artikels: articles,
    };
  },
  methods: {
    formMasuk() {
      this.formData = {
        id: this.generateId(),
        judul: "",
        image: "",
        date: "",
        content: "",
      };
      this.dialogFormAdd = true;
    },
    addData() {
      if (
        this.formData.judul &&
        this.formData.image &&
        this.formData.date &&
        this.formData.content
      ) {
        this.artikels.push({
          id: this.formData.id,
          judul: this.formData.judul,
          image: this.formData.image,
          date: this.formData.date,
          content: this.formData.content,
        });
        this.dialogForm = false;
      } else {
        alert("ID Tidak Ditemukan");
      }
    },
    getDatabyId(id) {
      const selectedArtikel = this.artikels.find(
        (artikel) => artikel.id === id
      );
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
    updateData() {
      if (
        this.formData.judul &&
        this.formData.image &&
        this.formData.date &&
        this.formData.content
      ) {
        const index = this.artikels.findIndex(
          (artikel) => artikel.id === this.formData.id
        );
        if (index !== -1) {
          this.artikels[index] = reactive({ ...this.formData });
          this.dialogEditForm = false;
        } else {
          alert("ID tidak ditemukan");
        }
      }
    },
    deleteData(id) {
      const deleteConfirm = window.confirm("Apakah anda ingin menghapus ini?");
      if (deleteConfirm) {
        this.artikels = this.artikels.filter((artikel) => artikel.id !== id);
      }
    },
    generateId() {
      return (this.artikels.length + 1).toString();
    },
  },
};
</script>

<style>
template {
  background-image: url("https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.pixground.com%2Fcolorful-background-dynamic-waves-ai-generated-4k-wallpaper%2F&psig=AOvVaw1_BTdFdEHXKR5_5mN1b2rV&ust=1699879599336000&source=images&cd=vfe&opi=89978449&ved=0CBEQjRxqFwoTCPCJgo-_voIDFQAAAAAdAAAAABAI");
  background-size: cover;
  height: 100vh;
}
</style>
