# Desafio Data Engineer

O objetivo desse desafio é analisar a sua capacidade em pesquisar, desenvolver um pipeline de dados através do Apache Beam e expor essas informações através de uma API em um ambiente dockerizado.
Critérios de avaliação:
- Qualidade do código
- Documentação do projeto
- Linha de raciocínio das consultas SQL

Espera-se como produto deste desafio o conjunto de  arquivos necessários para replicar a sua resposta além da documentação do projeto. Os dados necessários estão disponíveis no diretório /source_files onde existe um arquivo .zip onde existem dois arquivos públicos que foram extraídos do site do IBGE e do Coronavírus Brasil:

**Todas as etapas do projeto precisam ser documentadas, explicando a arquitetura proposta.**

## Tarefas



1. Criar um pipeline de dados através do Apache Beam em linguagem de programação Python que seja capaz de ler os arquivos EstadosIBGE.csv e HIST_PAINEL_COVIDBR.csv. O pipeline precisa ter 3 etapas:

    - Criar a tabela regiao no MySQL utilizando os dados do arquivo EstadosIBGE.csv. A tabela precisa ter as seguintes informações:
      * codigo_uf
      * uf
      * governador
    
    - Criar a tabela historico_covid no MySQL utilizando os dados do arquivo HIST_PAINEL_COVIDBR.csv. A tabela precisa ter as seguintes informações:
      * regiao
      * estado
      * municipio
      * cod_uf
      * data
      * casos_acumulados
      * casos_novos
      * obitos_acumulados
      * obitos_novos
      
    - Criar a tabela covid_regiao_periodo no MySQL utilizando os resultados dos passos anteriores. A tabela precisa ter as seguintes informações e o seu grande uso será filtrando por data ou data e uf:
      * data
      * regiao
      * estado
      * uf
      * governador
      * total_casos
      * total_obitos
      
      
      
2. Criação de uma API em Flask ou FastAPI que exponha uma lista com os resultados da tabela covid_regiao_periodo podendo receber como parâmetros um filtro de data inicial e final e uf.

    #### Resultado esperado:
    
    ```
    [
      {
        "regiao": "Sudeste",
        "estado": "Rio de Janeiro",
        "uf": "RJ",
        "data": "2021-01-01",
        "casos_acumulados": 99999,
        "casos_novos": 99999,
        "obitos_acumulados": 99999,
        "obitos_novos": 999999
       }
    ]
    ```
    
    
  3. Desenvolver consultas em SQL para realizar a exploração dos dados. Devem ser criadas consultas para responder a cada uma das seguintes perguntas
        - Qual foi o total de casos de covid por região?
        - Qual UF foi mais impactada por novos casos de covid em Agosto de 2020?
        - Quais regiões tiveram as maiores quantidade de óbitos em Setembro de 2020?
        - Qual foi o ranking de novos casos por governador no 4T de 2020?
        - Qual está sendo a 3a Região mais afetada por novos óbitos em 2021?
    
    
  
# Formato de entrega
O desafio proposto deverá ser entregue no seguinte formato:
  - O código deverá ser apresentado em um repositório privado do Github com o projeto desenvolvido. O repositório deverá estar bem documentado através de um arquivo README explicando a sua estrutura e passo-a-passo para replicação da resposta.
  - O projeto deverá ser entregue com um arquivo de configuração do Docker Composer que seja capaz de:
    * Subir um container com um banco de dados MySQL com as tabelas necessárias.
    * Execução do script em Apache Beam que será responsável por unir e tratar os arquivos disponibilizados, além de inserir os resultados no MySQL.
    * API que seja capaz de expor os dados processados pelo Apache Beam no MySQL.
    * Queries utilizadas para cada obter as respostas das perguntas do item 3.



