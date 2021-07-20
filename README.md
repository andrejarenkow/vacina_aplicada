# Quantas vacinas contra COVID-19 meu município aplicou?

As vacinas contra a COVID19 tem sido a grande esperança contra a pandemia. Os estados do país inteiro competem para ver quem aplica mais, uma corrida saudável, ao meu entender.
Mas você já parou para pensar quantas doses o seu município aplicou? De qual marca? Quantas primeiras doses? Quantas primeiras?

O governo federal disponibiliza uma API onde é possível baixar uma planilha completa sobre estes dados, lá é possível encontar os seguintes dados:
* "estabelecimento_razaoSocial"
* "vacina_dataAplicacao"
* "vacina_grupoAtendimento_codigo"
* "estabelecimento_valor"
* "@timestamp"
* "sistema_origem"
* "vacina_lote"
* "id_sistema_origem"
* "estalecimento_noFantasia"
* "paciente_endereco_coIbgeMunicipio"
* "paciente_endereco_coPais"
* "estabelecimento_uf"
* "paciente_nacionalidade_enumNacionalidade"
* "paciente_endereco_nmPais"
* "paciente_idade"
* "paciente_racaCor_codigo"
* "vacina_codigo"
* "paciente_endereco_nmMunicipio"
* "estabelecimento_municipio_nome"
* "vacina_fabricante_referencia"
* "estabelecimento_municipio_codigo"
* "vacina_grupoAtendimento_nome"
* "document_id"
* "@version"
* "data_importacao_rnds"
* "paciente_endereco_cep"
* "paciente_dataNascimento"
* "vacina_descricao_dose"
* "vacina_fabricante_nome"
* "vacina_categoria_codigo"
* "paciente_endereco_uf"
* "vacina_categoria_nome"
* "redshift"
* "vacina_nome"
* "paciente_racaCor_valor"
* "paciente_id"
* "paciente_enumSexoBiologico"

## Coletando os dados com Python

Para facilitar a vida de quem procura bancos de dados para analisar, eu criei um código no qual é possível extrair estes dados, informando o nome do município (sem acento) e a unidade federativa do mesmo.

O site da API e sua documentação estão em https://opendatasus.saude.gov.br/dataset/covid-19-vacinacao e o dado é aberto a todos.

Os dados estão hospedados na Elastic, e somente são possíveis de serem coletados em lotes de 10.000, ou seja, para um município muito grande, vai demorar.
O código coleta todos os dados disponíveis no Elastic sobre o município solicitado, pois possui um argumento chamado **Scroll_id**, que aponta para a continuidade daquele lote que já está sendo baixado.

Também inseri uma função de **print** no meio do loop, para saber se está funcionando ou não.
