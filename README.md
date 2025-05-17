# Relatório Técnico - Media Monks 2025

Relatório Técnico - Processo Seletivo Tech 2025 - Media Monks
1. Introdução

Este repositório contém o relatório técnico desenvolvido para o Processo Seletivo Tech 2025 da Media Monks. O objetivo foi realizar duas tarefas principais:

    Recuperar e corrigir dados de dois arquivos JSON (broken_database_1.json e broken_database_2.json) com informações de vendas de veículos e marcas.
    Gerar um relatório de desempenho de vendas utilizando consultas SQL no BigQuery.

A solução foi implementada em um notebook Jupyter (SQLtest_kymie(2).ipynb), utilizando Python para pré-processamento, SQL para consultas e SQLite como banco de dados em memória para prototipagem rápida.
2. Visão Geral do Projeto

O case simula um cenário real de gerenciamento de banco de dados de uma concessionária multimarcas. Os arquivos JSON contêm erros como caracteres especiais, tipos de dados incorretos e nomes de colunas inconsistentes. As tarefas incluíram:

    Corrigir formatos de dados e garantir integridade.
    Unir tabelas para criar um conjunto de dados coeso.
    Desenvolver consultas SQL para responder a perguntas de negócios sobre desempenho de vendas.
    Fornecer recomendações estratégicas baseadas na análise de dados.
    Documentar o processo e exportar os dados corrigidos.

3. Metodologia
3.1 Pré-processamento de Dados

O pré-processamento foi realizado utilizando a biblioteca pandas:

    Extração de Dados:
        broken_database_1.json foi carregado em um DataFrame vendas, contendo colunas como nome (nome do veículo), vendas (volume de vendas), valor_do_veiculo (preço), id_marca (ID da marca) e data (data da venda).
        broken_database_2.json foi carregado em um DataFrame marcas, com colunas id_marca e marca (nome da marca).
    Correção de Caracteres:
        Caracteres especiais (ex.: æ, ø, å) em nome e marca foram substituídos por letras padrão (ex.: Fiat corrigido de Fiæt).
    Conversão de Tipos de Dados:
        A coluna vendas foi convertida para formato numérico, tratando entradas inválidas e preservando valores ausentes.
    Padronização de Colunas:
        A coluna id_marca_ foi renomeada para id_marca para consistência entre os DataFrames.
    Configuração do Banco de Dados:
        Um banco SQLite em memória foi criado, e os DataFrames corrigidos foram carregados em tabelas SQL (vendas e marcas).

3.2 Desenvolvimento de Consultas SQL

As consultas SQL foram desenvolvidas para atender aos requisitos do case, utilizando funções utilitárias para executar modificações e consultas, compatíveis com a sintaxe do BigQuery e empregando recursos como CTEs, JOINs e funções de janela.
3.2.1 Recuperação de Dados (Tarefa 1)

    1.1 Correção de Campos de Veículos e Marcas:
        Correções de caracteres foram feitas no pré-processamento em Python, garantindo que nome e marca estivessem no formato correto antes do carregamento no banco.
    1.2 Conversão de Valores de Vendas:
        A coluna vendas foi pré-processada para formato numérico, permitindo agregações precisas em consultas SQL.
    1.3 Unindo Tabelas:
        As tabelas vendas e marcas foram unidas com um INNER JOIN, garantindo que apenas registros com id_marca correspondente fossem incluídos, preservando a integridade dos dados.
    1.4 Identificação de Marcas Sem Vendas:
        Um LEFT JOIN identificou marcas sem vendas. O resultado vazio indicou que todas as marcas tinham vendas associadas.
    1.5 Uso de CTE e Funções de Janela:
        Uma CTE calculou a média de vendas por marca, destacando marcas como Fiat, Volkswagen e Kia com desempenho acima da média.

3.2.2 Relatório de Vendas (Tarefa 2)

    2.1 Marca com Maior Volume de Vendas:
        Identificou a marca com maior volume de vendas, como Fiat ou Volkswagen, dependendo dos dados.
    2.2 Maior e Menor Receita Gerada por Veículo:
        Utilizou a função RANK() para destacar veículos com maior e menor receita, como Subaru Forester (maior) e Peugeot 307 (menor).
    2.3 Faixas de Preço de Venda:
        Gerou uma tabela com a distribuição de vendas por faixas de preço (intervalos de R$10.000), facilitando a análise de padrões de compra.
    2.4 Receita das 3 Marcas com Menores Tickets Médios:
        Identificou JaC Motors, Nissan e Chevrolet como as marcas com menores tickets médios, incluindo a receita total de cada uma.
    2.5 Relação entre os 5 Veículos Mais Vendidos:
        Analisou os cinco veículos mais vendidos (Fiat Mobi, Volkswagen Up, Kia Picanto, Peugeot 208, Toyota Corolla):
            Tendências de Mercado: Predominância de veículos compactos e econômicos, refletindo preferência por modelos acessíveis no Brasil.
            Percepção do Cliente: Fiat e Volkswagen são valorizadas por confiabilidade e assistência técnica; Kia e Peugeot atraem por design moderno.
            Características dos Veículos: Fiat Mobi e Volkswagen Up são ideais para uso urbano; Toyota Corolla destaca-se por durabilidade e revenda.

3.3 Recomendações Estratégicas

Uma consulta forneceu recomendações baseadas em volume de vendas, receita e meses ativos. Modelos como Fiat Mobi, Volkswagen Up e Kia Picanto foram classificados como "Modelo estrela - manter/maximizar" devido ao alto desempenho. Modelos com alta receita, mas baixo volume, como Subaru XV, têm potencial para aumentar vendas com estratégias de marketing.
3.4 Exportação de Resultados

Os dados corrigidos e análises foram exportados como arquivos JSON:

    dados_corrigidos.json: Conjunto completo com vendas e marcas unidas.
    marcas_corrigidas.json: Dados de marcas corrigidos.
    Análises adicionais: top_modelos.json, mix_produtos.json, elasticidade.json, recomendacoes.json.

4. Documentação

A documentação inclui:

    Códigos SQL:
        Correções via pré-processamento em Python e consultas para cada questão, explicadas no notebook.
    Arquivos Corrigidos:
        Dados Corrigidos
        Marcas Corrigidas
    Observações:
        O notebook apresenta seções claras com relatórios, análises estratégicas e recomendações acionáveis.

O repositório foi configurado para compartilhamento, com links para arquivos acessíveis no Google Drive, conforme solicitado.
5. Resultados

    Correção de Dados: Caracteres especiais corrigidos, tipos de dados convertidos e colunas padronizadas.
    Consultas SQL: Todas as consultas foram implementadas, utilizando CTEs, JOINs e funções de janela.
    Relatório de Vendas: Respostas detalhadas com análises baseadas em tendências de mercado e percepção do cliente.
    Recomendações: Identificação de modelos estrela e estratégias para maximizar receita e volume.
    Exportação: Dados e análises exportados como JSON, prontos para compartilhamento.

6. Conclusão

A solução atendeu a todos os requisitos do case, demonstrando proficiência em pré-processamento, consultas SQL complexas e análise estratégica. O uso de Python e SQLite facilitou a prototipagem, enquanto as consultas são compatíveis com BigQuery. A documentação organizada e as recomendações acionáveis refletem a capacidade de traduzir dados em insights de negócios.
7. Observações Finais

    A proibição de uso de ferramentas como ChatGPT foi respeitada.
    A documentação no notebook garante rastreabilidade e clareza.
    Os arquivos exportados estão prontos para integração ou análises futuras.

Data: 17 de maio de 2025

Hora: 14:53 (Horário de Brasília)
## Arquivos
- [Relatório Técnico (Markdown)](relatorio_tecnico.md)
- [Notebook Jupyter](SQLtest_kymie.ipynb)
- [Dados Corrigidos](dados_corrigidos.json)
- [Marcas Corrigidas](marcas_corrigidas.json)

## Acesso
- Visualize o relatório diretamente no GitHub ou via [Google Drive](#).
  
