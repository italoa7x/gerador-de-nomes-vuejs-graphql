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
                  <li
                    class="list-group-item"
                    v-for="prefix in prefixeds"
                    v-bind:key="prefix"
                  >
                    {{ prefix }}
                  </li>
                </ul>
                <br />
                <div class="input-group">
                  <input class="form-control" v-model="prefix" placeholder="Digite um prefixo" v-on:keyup.enter="addPrefix(prefix)"
                  />
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
                  <li
                    class="list-group-item"
                    v-for="sufix in sufixeds"
                    v-bind:key="sufix"
                  >
                    {{ sufix }}
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
              <li
                class="list-group-item"
                v-for="domain in domains"
                v-bind:key="domain"
              >
                {{ domain }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
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
			prefixeds: ["Air", "Micro"],
			sufixeds: ["Jordan", "Soft"],
			domains: ["AirJordan", "MicroSoft"],
		};
	},
	methods: {
		generate() {
			this.domains = [];
			this.prefixeds.forEach((pref) => {
				this.sufixeds.forEach((suf) => {
					this.domains.push(pref + suf);
				});
			});
		},
		addPrefix(prefix) {
			this.prefixeds.push(prefix);
			this.prefix = "";
			this.generate();
		},
		addSufix(sufix) {
			this.sufixeds.push(sufix);
			this.sufix = "";
			this.generate();
		},
	},
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
</style>
