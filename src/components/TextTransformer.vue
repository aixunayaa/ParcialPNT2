<template>
  <div>
    <form @submit.prevent>
      <input type="text" v-model="inputText" placeholder="Ingresá texto aquí" />
    </form>

    <p><strong>Caracteres ingresados:</strong> {{ charCount }}</p>

    <p><strong>1) Codificado:</strong> {{ codificado }}</p>
    <p><strong>2) Mayúsculas:</strong> {{ mayusculas }}</p>
    <p><strong>3) Minúsculas:</strong> {{ minusculas }}</p>
    <p><strong>4) Intercalado (empieza mayúscula):</strong> {{ intercaladoMay }}</p>
    <p><strong>5) Intercalado (empieza minúscula):</strong> {{ intercaladoMin }}</p>

    <hr />

    <div>
      <h3>Respuestas correctas:</h3>
      <ul>
        <li v-for="(respuesta, index) in respuestas" :key="index">
          Pregunta {{ index + 1 }}: {{ respuesta }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "TextTransformer",
  data() {
    return {
      inputText: "",
      respuestas: [
        "c) @click",
        "c) Los espacios adelante y atrás en una entrada de texto",
        "a) Definir el path y el componente activo para esa ruta",
      ],
    };
  },
  computed: {
    charCount() {
      return this.inputText.length;
    },
    codificado() {
      const mapVocales = { a: "u", e: "o", i: "i", o: "e", u: "a" };
      return this.inputText
        .toLowerCase()
        .split("")
        .map((c) => (mapVocales[c] ? mapVocales[c] : c))
        .join("");
    },
    mayusculas() {
      return this.inputText.toUpperCase();
    },
    minusculas() {
      return this.inputText.toLowerCase();
    },
    intercaladoMay() {
      return this.intercalar(this.inputText, true);
    },
    intercaladoMin() {
      return this.intercalar(this.inputText, false);
    },
  },
  methods: {
    intercalar(text, empiezaMayus) {
      let result = "";
      let mayus = empiezaMayus;
      for (let char of text) {
        if (/[a-zA-Z]/.test(char)) {
          result += mayus ? char.toUpperCase() : char.toLowerCase();
          mayus = !mayus;
        } else {
          result += char;
        }
      }
      return result;
    },
  },
};
</script>

<style scoped>
div {
  max-width: 500px;
  margin: 40px auto;
  background: #f9f9f9;
  padding: 25px 30px;
  border-radius: 12px;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.1);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #333;
}

input {
  padding: 12px 15px;
  font-size: 18px;
  width: 100%;
  margin-bottom: 20px;
  border: 2px solid #bbb;
  border-radius: 8px;
  transition: border-color 0.3s ease;
}

input:focus {
  border-color: #4f46e5; /* un violeta suave */
  outline: none;
  box-shadow: 0 0 8px #7c3aed88;
}

p {
  margin: 8px 0;
  font-size: 16px;
}

strong {
  color: #4f46e5;
}

hr {
  margin: 30px 0;
  border: none;
  border-top: 2px solid #ddd;
}

h3 {
  color: #4f46e5;
  margin-bottom: 15px;
}

ul {
  list-style-type: none;
  padding-left: 0;
}

li {
  background: #e0e7ff;
  margin-bottom: 8px;
  padding: 10px 15px;
  border-radius: 6px;
  font-weight: 600;
  color: #3730a3;
  transition: background-color 0.3s ease;
}

li:hover {
  background-color: #c7d2fe;
  cursor: default;
}
</style>
