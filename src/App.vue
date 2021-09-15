<template>
    <div id="app">
       <h1>Registrar Reclamação</h1>
		<div class="conteudo">
			<form v-if="submit" class="painel">
				<div class="cabecalho">Formulário</div>
				<Rotulo nome="E-mail">
					<input type="text" v-model.lazy.trim="usuario.nome">
				</Rotulo>
				<Rotulo nome="Senha">
					<input type="password" v-model="usuario.senha">
				</Rotulo>
				<Rotulo nome="Idade">
					<input type="number" v-model.number="usuario.idade">
				</Rotulo>
				<Rotulo nome="Mensagem">
					<textarea name="" cols="30" rows="5" v-model="usuario.mensagem"></textarea>
				</Rotulo>
				<Rotulo nome="Características do Problema">
					<span class="mr-4"><input type="checkbox" v-model="caracteristicas"
            value="reproduzivel"> Reproduzível</span>
					<span><input type="checkbox" v-model="caracteristicas"
            value="intermitente"> Intermitente</span>
				</Rotulo>
				<Rotulo nome="Qual produto?">
					<span class="mr-4"><input type="radio" value="web" v-model="produto"> Web</span>
					<span class="mr-4"><input type="radio" value="mobile" v-model="produto"> Mobile</span>
					<span><input type="radio" value="outro" v-model="produto"> Outro</span>
				</Rotulo>
				<Rotulo nome="Prioridade">
					<select v-model="prioridade">
						<option 
              :selected="prioridade.codigo === 'Baixa'"
              v-for="prioridade in prioridades" 
              :key="prioridade.codigo">
              {{ prioridade.nome }}
            </option>
					</select>
				</Rotulo>
				<Rotulo nome="Primeira Reclamação?">
					<Escolha v-model="escolha" :value="escolha"/>
				</Rotulo>
				<hr>
				<button @click="enviar" class="buttom">Enviar</button>
			</form>
			<div v-else class="painel">
				<div class="cabecalho">Resultado</div>
				<Rotulo nome="E-mail">
					<span>{{ usuario.nome }}</span>
				</Rotulo>
				<Rotulo nome="Senha">
					<span>{{ usuario.senha }}</span>
				</Rotulo>
				<Rotulo nome="Idade">
					<span>{{ usuario.idade }} {{tipo}}</span>
				</Rotulo>
				<Rotulo nome="Mensagem">
					<span style="white-space: pre;">{{ usuario.mensagem }}</span>
				</Rotulo>
				<Rotulo nome="Marque as Opções">
					<span>
            <ul>
              <li v-for="caracteristica in caracteristicas" :key="caracteristica">
                  {{caracteristica }}
              </li>
            </ul>
          </span>
				</Rotulo>
				<Rotulo nome="Qual produto?">
					<span>{{ produto }}</span>
				</Rotulo>
				<Rotulo nome="Prioridade">
					<span>{{ prioridade }}</span>
				</Rotulo>
				<Rotulo nome="Primeira Reclamação?">
					<span>{{escolha}}</span>
				</Rotulo>
        <button @click="voltar" class="buttom">Voltar</button>
			</div>
		</div>
    </div>
</template>

<script>
import Rotulo from './components/Rotulo.vue'
import Escolha from './components/Escolha.vue'
export default {
  components:{Rotulo, Escolha},
  computed:{
    tipo(){
      return typeof this.usuario.idade
    }
  },
  data () {
    return {
      caracteristicas:[],
      prioridade:'Baixa',
      prioridades:[
        {codigo: 1, nome: 'Baixa'},
        {codigo: 2, nome: 'Media'},
        {codigo: 3, nome: 'Alta'},
      ],
      produto: 'web',
      usuario:{
       email:'',
       senha:'',
       idade: 34
      },
      escolha: true,
      submit:true
    }
  },
  methods: {
    enviar(){
      this.submit = false
    },
    voltar(){
      this.submit = true
    }
  }
}
</script>

<style lang="scss">
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  
    display: flex;
    flex-direction: column;
  }

  body{
    background-color: #ECECEC;
  }

  .conteudo{
    display: flex;
  }

  .painel{
    flex: 1;
    background: #FFF;
    margin: 0px 10px;
    padding: 20px;
    border: 1px solid #AAA;
    border-radius: 5px;
  }
  
  .painel .cabecalho{
    width: 100%;
    background-color: #DDD;
    padding: 10px 0;
    border-radius: 5px;
    font-size: 1.2rem;
  }

 .buttom{
    float: right;
    margin: 10px 0px;
    padding: 10px 20px;
    font-size: 1.4;
    border-radius: 5px;
    color: #FFF;
    background-color: #2196F3;
  }

  #app h1 {
    font-weight: 200;
    margin: 20px;
    padding: 0px;
  }

  

</style>
