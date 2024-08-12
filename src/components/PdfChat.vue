<script setup>

</script>

<template>
  <div>
    <h1>Conversar com o PDF</h1>

    <form @submit.prevent="uploadPdf">
      <input type="file" @change="handleFileChange" />
      <button type="submit">Carregar PDF</button>
    </form>

    <div v-if="pdfText">
      <h2>Texto do PDF</h2>
      <textarea v-model="pdfText" rows="10" cols="50" readonly></textarea>

      <h2>Faça uma pergunta</h2>
      <form @submit.prevent="askQuestion">
        <input type="text" v-model="question" placeholder="Digite sua pergunta" />
        <button type="submit">Perguntar</button>
      </form>
    </div>

    <div v-if="response">
      <h2>Resposta</h2>
      <p>{{ response }}</p>
    </div>

    <div v-if="message">
      <p>{{ message }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      name: 'PdfChat',
      props: {
        msg: String
      },
      file: null,
      pdfText: '',
      question: '',
      response: '',
      message: ''
    };
  },
  methods: {
    handleFileChange(event) {
      this.file = event.target.files[0];
    },
    async uploadPdf() {
      const formData = new FormData();
      formData.append('file', this.file);

      try {
        const response = await axios.post('http://localhost:8080/api/pdf', formData, {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        });
        this.pdfText = true;
        this.message = response.data.message;
      } catch (error) {
        this.message = 'Erro ao carregar o PDF: ' + error.message;
      }
    },
    async askQuestion() {
      const formData = new FormData();
      formData.append('pergunta', this.question);
      try {
        const response = await axios.get('http://localhost:8080/api/chat/1', {
          params: {
            pergunta: this.question
          }
        });
        this.response = response.data;
      } catch (error) {
        this.message = 'Erro ao enviar a pergunta: ' + error.message;
      }
    }
  }
};



</script>



<style scoped>

</style>