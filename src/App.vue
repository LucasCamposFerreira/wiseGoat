<template>
  <div id="app">
    <header>
      <button
        class="btn-header"
        @click="openSite('https://www.devchallenge.com.br/')"
      >
        DevChallenge
      </button>
      <button
        class="btn-header"
        @click="openSite('https://github.com/LucasCamposFerreira/WiseGoat')"
      >
        Repository - Github
      </button>
    </header>
    <main>
      <div class="divConselho" v-if="!conselho">
        <h1 class="blabla">Wise Goat</h1>
        <button @click="conselho = !conselho" class="buttonConselho">
          Ask for advice
        </button>
      </div>
      <div class="divBode" v-if="!conselho">
        <img src="./assets/bodezinho.png" alt="BODE CONSELHEIRO" id="bodao" />
      </div>

      <div class="conselho" v-if="conselho">
        <div class="modal">
          <h2>Goat's advice 🧘</h2>
          <p>{{ frases.slip.advice }}</p>
          <br />
          <button class="closeButton" @click="getFrases()">
            Ask for other advice
          </button>
          <button @click="conselho = !conselho" class="closeButton">X</button>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      frases: "",
      conselho: false,
    };
  },
  methods: {
    getFrases() {
      fetch("https://api.adviceslip.com/advice")
        .then((r) => r.json())
        .then((r) => {
          this.frases = r;
        });
    },
    openSite(link) {
      window.open(`${link}`, "_blank");
    },
  },
  created() {
    this.getFrases();
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  border: 0;
}
main {
  display: flex;
  flex-direction: row;
  margin: 0 auto;
}
header {
  background: #72005f;
  width: 100%;
  margin: 0 auto;
  padding: 20px 20px;
}
.btn-header {
  border: none;
  border-radius: 25px;
  background: #baa193;
  padding: 10px;
  margin: 0 10px;
}
.divBode {
  width: 40%;
  padding: 0 50px;
}
#bodao {
  margin: 10px 0px;
  width: 50%;
  animation: go-back 2s infinite alternate;
}
.divConselho {
  margin: 20px 0;
  width: 70%;
  align-items: center;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  flex-wrap: wrap;
}
.buttonConselho {
  border: none;
  border-radius: 25px;
  width: 80%;
  background: #72005f;
  padding: 50px 180px;
  color: #baa193;
  font-family: monospace;
  font-size: 20px;
  font-weight: bold;
}
.conselho {
  margin: 0 0 0 20px;
}
.closeButton {
  border-radius: 25px;
  border: none;
  background: #72005f;
  color: #baa193;
  padding: 20px 30px;
  margin: 20px 20px;
}

@keyframes go-back {
  from {
    transform: translateY(100px) translateX(100px);
  }
  to {
    transform: translateY(0) translateX(100px);
  }
}
</style>
