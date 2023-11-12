# cnae_rfb
Atualização de base de dados de clientes  a partir de dados públicos da receita (CNAE), para fins de segmentação de clientes para análises  de negócios.

Empresa cliente, precisa compreender melhor o comportamento de cada mercado que atende. Partimos de uma base de cadastros de cliente em SQL, 
que contém 3 tabelas:  tabela pessoa ( onde estão informações cadastrais principais como id, razao social, cnpj, etc , que englobam clientes ,  
fornecedores e transportadoras), tabela clientes ( que contém informações específicas de clientes como data da primeira e  da ultima ultima compra entre outras)
e a tabela atividade ( com os campos codigo da atividade e descrição de atividade).

O ponto de partida foi analisar os dados de um backup fornecido pelo cliente apenas  com essas 3 tabelas, para verificar se as atividades cadastradas para cada cliente 
possuiam integridade e veracidade. Dessa análise constatou-se de que existiam duplicidades, atividades incoerentes e inadequadas  às necessidades da empresa. 

Assim, chegamos ao nosso problema de negócio a ser resolvido. Como fazer uma segmentação fidedigna e padronizada de clientes em atividades de mercadoo?

A solução proposta foi buscar dados públicos da receita federal, que contém o cadastro de todos os cnpjs das empresas brasileiras e seus dados cadastrais basicos, tendo
inclusive o CNAE ( cadastro nacioonal de atividades econômicas) principal de cada CNPJ, e cruzar com a base de clientes fornecida pela empresa cliente, para obter o CNAE
oficial de cada cliente na Receita, e  assim padronizar a segmentação de clientes em atividades, para posteriores análises e relatórios estratégicos. 

 A extração dos dados foi feita através de uma conexao ODBC pelo Power Query,  sendo realizada uma consulta SQL com junção  das 3 tabelas, considerando clientes que tenham data de primeira compra maior que 01/01/2023,  de modo a ter uma tabela resultante ( cadastro_clientes) como as colunas: codigo do cliente, razão social , nome fantasia, e concatenação das colunas codigo da atividade com descrição da atividade do cliente (atv_cliente).
 
 As tabelas se relacionam considerando que pes_codigo = cli_pescodigo e  pes_atvcodigo = atv_codigo.

Os dados da receita foram extraídos a partir de arquivos CSV disponívieis em:  https://dados.gov.br/dados/conjuntos-dados/cadastro-nacional-da-pessoa-juridica---cnpj.

Após o tratamento dos dados da tabelas extraídas , foi realizada no power query a mesclagem da tabela cadastro de clientes, de modo a trazer das tabelas da receita  o  CNAE corresponde a cada cnpj de cliente .

O resultado final foi  tabela base_clientes_cruzada, com as colunas : codigo do cliente, razão social , nome fantasia, atividade_clientne, codigo CNAE do cliente na receita, e descrição do CNAE do cliente na Receita e exportada para excel.  Foi gerada uma segmentação de dados suspensa da coluna atv_cliente e incluída uma coluna "cod_atv_corrigido" para que seja informada a atividade do cliente corrijida. 

 O objetivo  da segmentação suspensa da coluna atv_cliente, foi tornar   mais dinâmica a visualização de todos os clientes vinculados a uma determinada atividade para que seja analisada a coerência e correspondência da mesma com o CNAE do cliente na receita. Caso seja necessário corrigir a atividade do cliente, basta informar o codigo da atividade correta na coluna "cod_atv_corrigido".

 Após a empresa realizar a atualização e padronização das atividades de seus clientes a partir do CNAE da receita,  foi possível atualizar todas por meio de comando update no banco de dados.

 Uma vez com o banco de dados atualizado, conforme atividades adequadas aos CNAES da receita os dados estão prontos para análises específicas, como curva ABC  de atividades x valor de venda e diversas outras possibilidades de análises que envolvam segmentar clientes por atividades.

 

  

  






