<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>Nomeador de Projetos</h1>
      <br />
      <h6 class="text-secondary">
        Sistema gerador de nomes para <strong>Projeto</strong>
      </h6>
    </div>

    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>
              Prefixos
              <span class="badge badge-info">{{ prefixeds.length }}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefix in prefixeds" v-bind:key="prefix">
                    <div class="row">
                      {{ prefix }}
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="deletePrefix(prefix)"><span class="fa fa-trash"> </span></button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input class="form-control" v-model="prefix" placeholder="Digite um prefixo" v-on:keyup.enter="addPrefix(prefix)"/>
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefix(prefix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
            
          </div>

          <div class="col-md">
            <h5>
              Sufixos
              <span class="badge badge-info">{{ sufixeds.length }}</span>
            </h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixeds" v-bind:key="sufix">
                    <div class="row">
                      <div class="col-md">
                        {{ sufix }}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="deleteSufix(sufix)"><span class="fa fa-trash"> </span></button>
                      </div>
                    </div>
                    
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input class="form-control" v-model="sufix" placeholder="Digite um sufixo" v-on:keyup.enter="addSufix(sufix)"/>
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <br />
        <h5>
          Domínios <span class="badge badge-info">{{ domains.length }}</span>
        </h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                <div class="row">
                  <div class="col-md">
                    {{ domain.name }}
                  </div>
                  <div class="col-md text-right">
                    <a class="btn btn-info" target="_blank" v-bind:href="domain.checkout">
                      <span class="fa fa-shopping-cart"/>
                    </a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
    <h6 id="rodape">Feito por: <strong>Italo Alves 
      <a class="icones_redes_socais" href="http://www.github.com/italoa7x" target="_blank"><i class="fa fa-github" aria-hidden="true"></i></a>
      <a class="icones_redes_socais" href="http://www.instagram.com/italo_a1" target="_blank"><i class="fa fa-instagram" aria-hidden="true"></i></a>
      </strong></h6>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
	name: "App",
	data: function() {
		return {
			prefix: "",
			sufix: "",
			prefixeds: ["Arib", "App"],
			sufixeds: ["nb", "le"],
		};
	},
	methods: {
		addPrefix(prefix) {
			this.prefixeds.push(prefix);
			this.prefix = "";
		},
		addSufix(sufix) {
			this.sufixeds.push(sufix);
			this.sufix = "";
		},
		deleteSufix(sufix){
			this.sufixeds.splice(this.sufixeds.indexOf(sufix), 1);
		},
		deletePrefix(prefix){
			this.prefixeds.splice(this.prefixeds.indexOf(prefix), 1);
		}
	},
	computed: {
		domains() {
			const domains = [];
			for(const prefix of this.prefixeds){
				for(const suf of this.sufixeds){
					const name = prefix + suf;
					const url = name.toLowerCase();
					const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;
					domains.push({
						name,
						checkout
					});
				}
			}
			return domains;
		}
	}
};
</script>

<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}
#main {
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
#rodape{
  margin-left: 20px;
}
.icones_redes_socais {
  margin-left: 10px;
}
</style>
