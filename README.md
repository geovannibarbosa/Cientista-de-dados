Avaliação - Cientista de Dados I
Nome: Geovanni Barbosa Reis
Questões:
1.1 - Sua tarefa é criar: Uma estrutura de diretórios e nomenclatura de arquivos que permita armazenar as consultas de modo coerente
Resposta:

Para criar uma estrutura de diretórios e nomenclatura de arquivos que permita armazenar as consultas de modo coerente, é necessário primeiramente analisar o que será consultado e como será consultado. Conforme disponibilizado anteriormente no exercício, os dados serão utilizados em um painel que responde perguntas do tipo: "Qual a quantidade de soja que o Brasil exportou para a China em 2020", sendo assim, na estrutura de diretórios deve-se levar em consideração essas informações (país de origem, país destino, ano).

A estrutura sugerida é a seguinte:

BRA/ARG/2019.txt representando respectivamente o país de origem, o país destino e o ano da busca.
BRA/ARG/2020.txt
BRA/AFG/2019.txt
1.2 - Liste as etapas necessárias para integração de 3 anos (2019~2021) de comércio exterior
Resposta:

Definir o objetivo e ferramentas a serem utilizadas

Objetivo: Buscar as informações da API, garantir a integridade dos dados e salvá-los de forma organizada.
Ferramentas: Python, bibliotecas requests (para busca de dados), pandas (para tratamento dos dados) e os (para direcionamento dos arquivos).
Definir as consultas válidas

Verificar parâmetros para evitar consultas inválidas (ex: BRA, BRA, 2020).
Definir as classes, métodos e atributos

Utilizar programação orientada a objetos para tornar o código reutilizável, modular e de fácil manutenção.
Testar a API

Realizar alguns requests da API e trabalhar com eles em um dataframe para entender o funcionamento.
Listar os países e anos para consulta

Exemplo: lista_paises=[BRA, ARG, AFG, ...]; anos=[2019, 2020, 2021].
Solicitação e tratamento dos dados

Utilizar requests e pandas para enviar as listas de países e anos para a API e retornar os dados em um dataframe.
Salvar os arquivos

Utilizar os e pandas para salvar o dataframe em arquivos de texto.
1.3 - Qual/Quais arquivo(s) da sua base de dados respondem a questão: 'Qual a quantidade de soja o Mundo importou do Brasil em 2020?'
Resposta:

O arquivo que responde à questão "Qual a quantidade de soja o Mundo importou do Brasil em 2020?" é:

BRA/WLD/2020.txt
1.4 - Sua base de dados alimenta um painel que possui informações de comércio exterior entre países – e também mundo. As consultas de comércio exterior podem ser feitas com os parâmetros M (‘mês’) ou A (‘ano’). A consulta M representa um report dos meses disponíveis no ano até então. A consulta A representa o report final/completo das imp/exp em determinado ano. Considere que cada país escolhe uma data “aleatória” do primeiro trimestre do novo ano para realizar o report final/completo das suas exportações e importações anuais do ano anterior.
Resposta:

Definir o objetivo e ferramentas a serem utilizadas

Objetivo: Atualizar as informações garantindo integridade e organização dos dados.
Ferramentas: requests, pandas, os, schedule e datetime.
Definir as consultas válidas

Evitar consultas inválidas.
Definir classes, métodos e atributos

Utilizar programação orientada a objetos.
Testar a API

Realizar algumas consultas para entender o formato de solicitação e recebimento de dados.
Listar os países, meses e anos para consulta

Exemplo: lista_paises=[BRA, ARG, AFG, ...]; ano=[2019, 2020, 2021]; mes=['01', '02', '03', ...].
Definir as datas de report final

Estabelecer datas "aleatórias" no primeiro trimestre de cada ano para cada país (ex: data_report = {'BRA': '2025-03-15'}).
Verificação de datas para realização da consulta

Verificar se a data é válida (posterior à data de report) e se a consulta busca dados anuais ou mensais.
Salvar os arquivos

Salvar os arquivos das consultas em arquivos de texto representando dados anuais ou mensais.
Agendamento de atualizações

Utilizar a ferramenta schedule para agendar a execução das consultas.
2 - Considere os arquivos públicos da Receita Federal disponíveis em: Receita Federal. A página é atualizada, na média, 1 vez ao mês: os nomes dos arquivos são fixos. Suponha que você precise automatizar o processo de baixar, empilhar e manter atualizado os arquivos de empresas (0~9). Considere que o site é instável, portanto, o arquivo baixado pode estar corrompido. Liste as etapas necessárias para que o dataset de empresas esteja sempre atualizado.
Resposta:

Definir o objetivo e as ferramentas

Objetivo: Automatizar o download, verificar a integridade e atualizar automaticamente os arquivos de empresas.
Ferramentas: requests, pandas, os, schedule, datetime, hashlib e zipfile.
Definir o nome dos arquivos

Exemplo: [f"Empresa{num}.zip" for num in range(10)].
Verificar a integridade dos arquivos

Utilizar hashlib para validar os arquivos. Se corrompido, tentar nova busca (até 3 tentativas). Se ainda corrompido, notificar o analista.
Baixar os arquivos

Utilizar requests para salvar os arquivos localmente.
Organizar os dados

Adotar uma nova estrutura de organização para salvar os dados.
Extrair e processar os arquivos

Utilizar zipfile e os para extrair e direcionar os arquivos.
Agendamento das atualizações

Utilizar schedule para agendar a execução periódica do código.
3 - Escreva uma consulta SQL que retorne, para cada funcionário, o nome do departamento em que ele trabalhou pela primeira vez (baseado na data de início de trabalho), o nome do departamento onde ele está atualmente trabalhando, e a quantidade de departamentos diferentes em que ele já trabalhou. Use as tabelas employees, departments, e employee_department_history.
Resposta:

sql
Copiar código
SELECT 
    e.employee_name AS funcionario,
    MIN(d1.department_name) AS primeiro_departamento,
    MAX(CASE WHEN edh.end_date IS NULL THEN d2.department_name END) AS atual_departamento,
    COUNT(DISTINCT edh.department_id) AS contagem_departamentos
FROM 
    employees AS e
INNER JOIN
    employee_department_history AS edh ON e.employee_id = edh.employee_id
INNER JOIN
    departments AS d1 ON d1.department_id = edh.department_id
LEFT JOIN
    departments AS d2 ON d2.department_id = edh.department_id AND edh.end_date IS NULL
GROUP BY 
    e.employee_name;
4 - O arquivo exemplo1.parquet possui 7GB. O tempo de leitura e retorno de 1 linha específica são 5s - utilizando processamento paralelo (pyspark) em cluster. Contudo, você precisa criar uma API com recursos bem mais modestos, isto é, menor poder de processamento - mantendo o tempo de consulta rápido. Liste as alterações e procedimentos necessários para realizar isso.
Resposta:

Pré-processamento

Criar índices no arquivo Parquet para acelerar a busca ou converter para CSV.
Armazenamento

Converter os dados para um banco otimizado para consultas rápidas (ex: SQLite) ou utilizar cache para consultas frequentes.
Otimização

Utilizar bibliotecas eficientes para ler os dados Parquet ou fragmentar os dados para ler apenas o necessário.
Implementação da API

Utilizar frameworks leves como Flask.
Monitoramento

Verificar o desempenho da API e ajustar para manter o tempo de resposta estimado.
5 - Você foi instruído a criar um modelo de regressão baseado em um modelo econométrico. Ao terminar a implementação você verificou que o resultado está abaixo do esperado. Liste o que poderia ser feito para melhorar o resultado.
Resposta:

Verificar a coerência dos dados.
Tratar outliers que possam estar alterando o resultado.
Verificar se todas as variáveis relevantes foram consideradas.
Aplicar regularização (ex: Lasso) para evitar overfitting.
Realizar validação cruzada.
Ajustar o modelo com base nas análises e melhorias implementadas.
6 - ELT e ETL são termos comuns na rotina de trabalho de especialistas em Soluções de Tecnologia da Informação, justamente por representarem estratégias de pipelines de integração de dados em um determinado projeto. Sobre esses procedimentos, é correto afirmar que:
Resposta:

d) **Estrutura de dados em nuvem são
