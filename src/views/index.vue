<template>
  <Navbar />
  <div class="container-fluid h-100">
    <div class="row h-100 mt-2">
      <div class="col-md-12 h-100 d-flex justify-content-center">
        <div class="col-md-12 rounded px-5 py-4 shadow bg-white text-left">
          <h2 class="text-center">Form Penerima Bantuan Sosial (Bansos)</h2>
          <Form />
        </div>
      </div>
    </div>
  </div>
  <Footer />
</template>

<script>
import Navbar from "../components/navbar.vue";
import Form from "../components/form.vue";
import Footer from "../components/footer.vue";

export default {
  name: "App",
  components: {
    Navbar,
    Form,
    Footer
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}
</style>
