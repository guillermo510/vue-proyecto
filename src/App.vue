<script>
export default {
  components: {},
  data() {
    return {
      email: "",
      password: "",
      usuarioActual: { email: "", password: "" },
      mostrarLogin: true,
      mostrarFormulario: false,
      publicaciones: [],
      titulo: "",
      descripcion: "",
      imagen:'',
    };
  },
  methods: {
    guardarUsuarioActual() {
      this.usuarioActual = { email: this.email, password: this.password };
      this.mostrarLogin = false;
      this.mostrarFormulario = true;
    },
    hacerPublicacion() {
      this.publicaciones.push({
        email: this.email,
        titulo: this.titulo,
        descripcion: this.descripcion,
        imagen: this.imagen,
      });
      this.titulo = "";
      this.descripcion = "";
      this.imagen = '';
    },
    cerrarSesion() {
      this.email = "";
      this.password = "";
      this.mostrarLogin = true;
      this.mostrarFormulario = false;
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-md-2"></div>
      <div class="col-md-8">
        <form
          v-if="mostrarLogin == true"
          class="bg-white p-3 border rounded shadow"
          id="login"
          action=""
          v-on:submit.prevent="guardarUsuarioActual"
        >
          <div class="mb-3">
            <label for="email" class="form-label">Email</label>
            <input
              v-model="email"
              type="email"
              class="form-control"
              id="email"
              placeholder="usuario@email.com"
            />
          </div>
          <div class="mb-3">
            <label for="password" class="form-label">Password</label>
            <input
              v-model="password"
              type="password"
              class="form-control"
              id="password"
              placeholder="Ingrese su contraseña"
            />
          </div>
          <button class="btn btn-info text-light" type="submit">Enviar</button>
        </form>
        <div v-if="mostrarFormulario == true">
          <div class="row">
            <button v-on:click="cerrarSesion" class="mt-5 mb-5 btn btn-info text-light" id="cerrarSesion">
              Cerrar sesión
            </button>
            <div class="col-md-1"></div>
            <form
              class="bg-white col-md-10 border rounded p-3 shadow"
              id="formularioPublicacion" 
              action=""
              v-on:submit.prevent="hacerPublicacion"
            >
              <div class="mb-3">
                <label for="titulo" class="form-label">Título</label>
                <input
                  v-model="titulo"
                  type="titulo"
                  class="form-control"
                  id="titulo"
                  placeholder="Título de la publicación."
                />
              </div>
              <div class="mb-3">
                <label for="floatingTextarea" class="form-label"
                  >Publicación</label
                >
                <textarea
                  v-model="descripcion"
                  class="form-control"
                  placeholder="Escriba su publicación."
                  id="floatingTextarea"
                ></textarea>
              </div>
              <div class="mb-5">
                <label for="imagen" class="form-label"
                  >URL de imágen</label
                >
                <textarea
                  v-model="imagen"
                  class="form-control"
                  placeholder="URL de la imágen a publicar."
                  id="imagen"
                ></textarea>
              </div>
              <button class="btn btn-info text-light" type="submit">
                Pubicar
              </button>
            </form>
            <div class="col-md-1"></div>
          </div>
          <div class="row mb-5">
            <div v-for="publicacion of publicaciones" class="mt-5 card text-black shadow" id="publicaciones">
              <div class="card-body">
                <div class="col-md-6"></div>
                <h6>{{publicacion.email}} dice:</h6>
                <h5 class="card-title">{{publicacion.titulo}}</h5>
                <p class="card-text">
                    {{publicacion.descripcion}}
                </p>
                <img v-bind:src=publicacion.imagen class="card-img-top" alt="Imágen de publicación">
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-2"></div>
    </div>
  </div>
</template>

<style>

    body{
      background-color: #f2f2f2;
    }

    img{
        max-height: 500px;
    }

    #login {
      margin: 15%;
    }

    #cerrarSesion{
      width: 100%;
    }
</style>
