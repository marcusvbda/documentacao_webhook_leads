## Documentação webhook Ezcore Leads

para comunicar com o webhook Ezcore Leads CRM deve-se enviar um request **POST**
para a seguinte rota, substituindo os respectivos parâmetros **client_id** e **secret_id** 

    http://leads.ezcore.com.br/api/integration/set/leads/{client_id}/{secret_key}

deve-se enviar um **JSON** formatado com o exemplo abaixo
```
{
     "leads" : [{
         "id" : "id_do_lead",
		 "doc_number" : "numero_do_documento",
		 "cod_type" : "tipo_do_documento_comumente_cpf",
		 "status_value", "status_value_lista_de_opcoes_abaixo",
		 "date" : "data_de_agendamento_opcional",
		 "time" : "hora_de_agendamento_opcional",
         "email" : "email_do_lead",
         "personal_phone" : "telefone_fixo",
         "mobile_phone" : "telefone_movel",
         "name" : "nome_do_lead",
         "cidade" : "cidade_do_lead",
         "city" : "cidade_do_lead",
         "state" : "estado_do_lead",
         "course" : "curso_de_preferencia",
	 "tags" : ["tag1","tag2","tag3"]
    }]
}
```

Sendo que apenas "**tags**" um campo opcional e "**time**" e "**date**" condicionalmente opcional.

### Lista de opções de Status
para o index "**status_value** do json, deve-se usar o value de uma das opções abaixo
```
[
	{
		"value" : "sem-agendamento",
		"name" : "Sem Agendamento"
	},
	{
		"value" : "agendado",
		"name" : "Agendado"
	},
	{
		"value" : "cancelado",
		"name" : "Cancelado"
	},
	{
		"value" : "finalizado",
		"name" : "Finalizado"
	},
	{
		"value" : "vestibular",
		"name" : "Vestibular"
	}
]
```
No caso de status "**agendado**" ou "**vestibular**", os campos "**date**" e "**time**" passam a ser obrigatórios pois são referentes a data e hora de agendamento dos mesmos.


Toda e qualquer informação adicional pode ser incluída no json e o **Ezcore Leads** essa informação será cadastrada com campo adicional, acessível durante a operação do lead.

O index "**leads**" do json é um **array**, sendo assim, um request poderá conter N leads em seu conteúdo e deverá ser organizado da seguinte forma neste caso:
```
{
	"leads" : [{
	    	//conteudo do lead 
	    },
	    {
	    	//conteudo do lead 
	    },
	    {
	    	//conteudo do lead 
	    },
	    {
	    	//conteudo do lead 
	    }
	    ....
	}]
}
```


Caso suas credenciais sejam de homologação você apenas receberá respostas positivas ou negativas, contendo o erro que deve ser corrigido no request em caso negativo e em todos os casos seguindo o seguinte padrão

```
{ 
	"success" : true,
	"message" : "lorem ispum",
	"data" : null
} 
```

sendo o conteúdo de **success** ```true``` ou ```false```, **message** uma mensagem referente ao request e **data** conteúdo de retorno caso seja necessário, o padrão sempre será ```null```
