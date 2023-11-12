# cnae_rfb
Atualização de base de dados de clientes  a partir de dados públicos da receita (CNAE), para fins de segmentação de clientes para análises  de negócios. 

Empresa cliente, precisa compreender melhor o comportamento de cada mercado que atende. Partimos de uma base de cadastros de cliente em SQL, 
que contém 3 tabelas:  tabela pessoa ( onde estão informações cadastrais principais como id, razao social, cnpj, etc , que englobam clientes ,  
fornecedores e transportadoras), tabela clientes ( que contém informações específicas de clientes como data da primeira e  da ultima ultima compra entre outras)
e a tabela atividade ( com os campos codigo da atividade e descrição de atividade).

O ponto de partida foi analisar os dados de um backup fornecido pelo cliente apenas  com essas 3 tabelas, para verificar se as atividades cadastradas para cada cliente 
possuiam integridade e veracidade. Dessa análise constatou-se de que existiam duplicidades, atividades incoerentes e inadequadas  às necessidades da empresa. 

Assim, chegamos ao nosso problema de negócio a ser resolvido. Como fazer uma segmentação fidedigna padronizada de clientes em atividades de mercadoo?

A solução proposta foi buscar dados públicos da receita federal, que contém o cadastro de todos os cnpjs das empresas brasileiras e seus dados cadastrais basicos, tendo
inclusive o CNAE ( cadastro nacioonal de atividades econômicas) principal de cada CNPJ, e cruzar com a base de clientes fornecida pela empresa cliente, para obter o CNAE
oficial de cada cliente na Receita, e  assim padronizar a segmentação de clientes em atividades, para posteriores análises e relatórios estratégicos. 



