<template>
  <div v-if="userRole === 'Admin'">
    <nav class="sidebar">
      <br />
      <ul class="sidebar-top sidebar-bg">
        <li class="sidebar-toggle navbar-brand d-flex align-items-center">
          <img
            src="../assets/../assets/img/Logo.png"
            alt="Logo Desa"
            height="50"
            class="me-3"
          />
          <div>
            <span class="font-weight-bold nama-desa">Desa Bahomoleo</span>
            <span class="sub-text">Kab. Morowali</span>
          </div>
        </li>
      </ul>

      <div class="sidebar-content">
        <ul class="sidebar-list">
          <li class="sidebar-link">
            <router-link to="/beranda-admin" class="menu-item"
              >Beranda</router-link
            >
            <router-link to="/warga-desa" class="menu-item">
              Warga Desa</router-link
            >
            <router-link to="/berita-desa" class="menu-item"
              >Berita Desa</router-link
            >
            <router-link to="/umkm-desa" class="menu-item"
              >UMKM Desa</router-link
            >

            <router-link to="/wisata-desa" class="menu-item"
              >Wisata Desa</router-link
            >

            <Dropdown title="Pemerintahan" class="tulisan" />

            <router-link to="/potensi-desa" class="menu-item"
              >Potensi Desa</router-link
            >

            <router-link to="/kreatifitas-desa" class="menu-item"
              >Kreatifitas Desa</router-link
            >

            <router-link to="/warga-desa" class="menu-item"
              >Wilayah Desa</router-link
            >

            <router-link to="/warga-desa" class="menu-item"
              >Layanan Desa</router-link
            >
          </li>
        </ul>

        <div class="sidebar-bottom">
          <button
            @click="clearLocalStorage"
            class="btn panjang-tombol-login1 btn-light text-tombol text-start"
          >
            <span class="tulisan"
              ><v-icon name="ai-academiaSquare" />Logout</span
            >
          </button>
        </div>
      </div>
    </nav>
  </div>

  <div v-else-if="userRole === 'Warga'">
    <nav class="sidebar-admin">
      <h1>INI JADI SIDEBAR WARGA</h1>
    </nav>
  </div>

  <div v-else>
    <nav class="menu">
      <div class="navbar navbar-expand-lg navbar-dark bg-transparent">
        <div className="container">
          <router-link to="/" class="navbar-brand d-flex align-items-center">
            <img
              src="../assets/../assets/img/Logo.png"
              alt="Logo Desa"
              height="50"
              class="me-3"
            />
            <div>
              <span class="font-weight-bold nama-desa">Desa Bahomoleo</span>
              <span class="sub-text">Kab. Morowali</span>
            </div>
          </router-link>

          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarNav"
            aria-controls="navbarNav"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>

          <div class="collapse navbar-collapse"></div>
          <div
            class="collapse navbar-collapse justify-content-center"
            id="navbarNav"
          >
            <div class="menu-item"><a href="/">Beranda</a></div>
            <Dropdown title="Profil Desa" :items="profil" />
            <div class="menu-item">
              <a href="/pemerintah-desa">Pemerintah Desa</a>
            </div>
            <div class="menu-item"><a href="/informasi">Informasi</a></div>
            <Dropdown title="Media" :items="media" />
            <Dropdown title="Destinasi" :items="destinasi" />
            <div class="menu-item"><a href="/idm">IDM</a></div>
            <div class="menu-item"><a href="/data-desa">Data Desa</a></div>
          </div>

          <div
            class="collapse navbar-collapse justify-content-end"
            id="navbarNav"
          >
            <div class="d-flex">
              <button
                class="btn panjang-tombol-login btn-light me-2 text-tombol"
              >
                <router-link to="/login" class="nav-link router-link-underline"
                  >Login</router-link
                >
              </button>
            </div>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import Dropdown from "./Dropdown.vue";

export default {
  name: "navbar",
  components: {
    Dropdown,
  },
  data() {
    return {
      profil: [
        {
          title: "Sejarah Desa",
          link: "/sejarah",
        },
        {
          title: "Wilayah Desa",
          link: "/wilayah",
        },
        {
          title: "Potensi Desa",
          link: "/potensi",
        },
      ],
      media: [
        {
          title: "Galeri Foto",
          link: "/galeri-foto",
        },
        {
          title: "Berita",
          link: "/berita",
        },
        {
          title: "Artikel",
          link: "/artikel",
        },
      ],
      destinasi: [
        {
          title: "UMKM",
          link: "/umkm",
        },
        {
          title: "Wisata",
          link: "/wisata",
        },
      ],
    };
  },

  created() {
    this.checkUserRole();
    window.addEventListener("storage", this.handleStorageChange);
  },
  destroyed() {
    window.removeEventListener("storage", this.handleStorageChange);
  },
  methods: {
    clearLocalStorage() {
      localStorage.clear();
      console.log("Localstorage dibersihin!");
      this.userRole = "";
      location.reload();
    },

    checkUserRole() {
      this.userRole = localStorage.getItem("role_pengguna");
      if (this.userRole === "Admin") {
        this.$router.push("/beranda-admin");
      }

      if (this.userRole === "Warga") {
        this.$router.push("/beranda-warga");
      }
    },
    handleStorageChange(event) {
      if (event.key === "role_pengguna") {
        this.checkUserRole();
      }
    },
  },
  watch: {
    userRole(newRole) {
      if (newRole === "Admin") {
        this.$router.push("/beranda-admin");
      }

      if (newRole === "Warga") {
        this.$router.push("/beranda-warga");
      }
    },
  },
};
</script>

<style>
.sidebar {
  width: 285px;
  height: 100vh;
  position: fixed;
  justify-content: center;
  top: 0;
  left: 0;
  z-index: 999;
  background-color: #003366;
  margin-left: -1%;
  padding: 0px 30px;
}

.sidebar-top {
  width: 100%;
  height: 90px;
  line-height: 30px;
}

.sidebar-toggle {
  width: 90%;
  height: 90px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: none;
}

.sidebar-list {
  display: flex;
  padding: 5px 15px;
  row-gap: 1.5rem;
  flex-direction: column;
  border: none;
}

ul {
  list-style-type: none;
}

/* User */
* {
  font-family: "Poppins", sans-serif !important;
}

.menu {
  background-color: #003366;
  line-height: 2;
  box-shadow: inset 0px 0px 20px 0px rgba(0, 0, 0, 0.2);
}

.sub-text {
  font-size: 0.7em;
  opacity: 0.7;
  display: block;
  margin-top: -10px;
  color: #ffffff;
}

.nama-desa {
  font-weight: bold;
  color: rgb(255, 255, 255);
}

.text-tombol {
  font-weight: bold;
  color: rgba(255, 255, 255, 0.2);
  font-size: 15px;
}

.panjang-tombol-login {
  width: 100px;
}

.menu-item a {
  color: white;
  text-decoration: none;
}
.menu-item {
  color: white;
  padding: 10px 15px;
  position: relative;
  text-align: center;
  border-bottom: 3px solid transparent;
  display: flex;
  transition: all 0.3s ease;
  text-decoration: none;
}

.menu-item.active,
.menu-item:hover {
  background-color: white;
  border-bottom-color: #003366;
  border-radius: 20px;
  color: #003366;
}

.menu-item.active a,
.menu-item:hover a {
  color: #003366;
}

.sidebar-bottom {
  color: white;
  padding: 80px 25px;
  position: relative;
  text-align: center;
  border-bottom: 3px solid transparent;
  display: flex;
  transition: all 0.3s ease;
}

.sidebar-buttom span {
  color: inherit;
  text-decoration: none;
}

.sidebar-buttom.active,
.sidebar-buttom:hover {
  background-color: white;
  border-bottom-color: #003366;
  border-radius: 20px;
}

.sidebar-buttom.active span,
.sidebar-buttom:hover span {
  color: #003366;
}

.panjang-tombol-login1 {
  width: 250px;
}
</style>
