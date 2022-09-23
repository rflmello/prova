<template>
  <div>
    <div>
      <h2>Alunos e notas</h2>
  
      <form @submit.prevent="salvar()">
  

        <label for="nome"> Nome</label>
        <input type="text" id="nome" v-model="nome" size="30"><br/>
  
        <label for="nota1">Nota 1</label>
        <input type="number" id="nota1" v-model="nota1"><br/>

        <label for="nota3">Nota 3</label>
        <input type="number" id="nota3" v-model="nota2"><br/>

        <label for="nota3">Nota 3</label>
        <input type="number" id="nota3  " v-model="nota3"><br/>

        <input type="submit">
      </form>
  
      <table>
        <tr>
          <th>Nome</th>
          <th>Nota 1</th>
          <th>Nota 2</th>
          <th>Nota 3</th>
          <th>Média</th>
          <th>Situação</th>
        </tr>
        <tr v-for="p in projetos" :key="p.nome"> 
          <td>{{ p.nome }}</td>
          <td>{{ p.nota1 }} </td>
          <td>{{ p.nota2 }} </td>
          <td>{{ p.nota3 }} </td>
          <td>{{ p.media }} </td>
          <td>{{ p.situacao }} </td>
        </tr>
      </table>
    </div>
    </div>
  
  
  </template>
  
  <script>
  
  export default {


    data() {
      return {
        projetos: [

        ],
        nome: '',
        nota1: null,
        nota2: null, 
        nota3: null,
        media: null,
        situacao: null
      }
    },
    methods: {
      selecionar(projeto) {
        this.selected = projeto
        this.nome = projeto.nome
        this.nota1 = projeto.nota1
        this.nota2 = projeto.nota2
        this.nota3 = projeto.nota3
        this.situacao = projeto.situacao
      },

      validar() {
        const achou = this.projetos
                .some(p => p != this.selected && p.nome == this.nome)  
        if (achou) {
          alert('Aluno já existe')
          return false
        }
        return true
      },

      getSituacao() {
        if (this.getMedia() >= 7) {
          this.situacao = 'Aprovado'
        } else {
          this.situacao = 'Reprovado'
        }
        return this.situacao
      },

      getMedia() {
        this.media = (this.nota1 + (this.nota2 * 2) + (this.nota3 * 3))/7
        return this.media
      },
  
      inserir() {
        if (!this.validar()) 
          return false;
        this.projetos.push(
          {
            nome: this.nome,
            nota1: this.nota1,
            nota2: this.nota2,
            nota3: this.nota3,
            media: this.getMedia(), //(this.nota1 + (this.nota2 * 2) + (this.nota3 * 3))/7,
            situacao: this.getSituacao()

          }
        )
        return true
      },
  
 
      salvar() {
  
        let sucesso = this.inserir();
        if (sucesso) {
          this.limparCampos()
        }
        
      },
      limparCampos() {
         this.selected = null
         this.nome = ''
         this.nota1 = null
         this.nota2 = null
         this.nota3 = null
       },
    
    },
    
    computed: {
  
    }
  }
  
  </script>
  
  <style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  
  .selected {
    background-color: rgb(236, 46, 78);
  }
  </style>
  