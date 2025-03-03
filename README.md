# ETL-Python

Descrição do Projeto - ETL para Processamento de Dados de Vendas

Este projeto implementa um processo de ETL (Extract, Transform, Load) com o objetivo de ler e  extrair dados de varios arquivos de vendas, transformá-los para um formato adequado e carregá-los em um banco de dados SQL Server. O processo segue as etapas básicas de ETL, que incluem a criação de tabelas dimensionais e uma tabela fato no banco de dados, sendo essas as principais operações realizadas:
Etapas do Processo:

    Extração (Extract):
        Os dados são extraídos de um arquivo CSV ou DataFrame existente. A coluna 'Categoria', 'Produto', 'MetodoPagamento', 'DataVenda', entre outras, são extraídas e organizadas para posterior transformação.

    Transformação (Transform):
        Criação de Tabelas Dimensionais:
            DimCategoria: A tabela dimensional para categorias de produtos é criada com um identificador único CategoriaID.
            DimProduto: A tabela dimensional para produtos é criada com um identificador único ProdutoID.
            DimMetodoPagamento: A tabela dimensional para métodos de pagamento é criada com um identificador único MetodoPagamentoID.
            DimTempo: A tabela dimensional de tempo é criada a partir da coluna DataVenda. A data é transformada em DataID e as informações de ano, mês e dia são extraídas e associadas.
        Cálculo de Impostos:
            Um cálculo de imposto é realizado para cada venda, dependendo do valor total:
                10% para valores superiores a R$ 1000.
                5% para valores entre R$ 500 e R$ 1000.
                0% para valores abaixo de R$ 500.

    Carregamento (Load):
        Após a transformação, as tabelas dimensionais são carregadas no banco de dados SQL Server usando SQLAlchemy.
        Além disso, a tabela FatoVenda é criada a partir das junções das tabelas dimensionais e dos dados de vendas, contendo as colunas de ProdutoID, CategoriaID, MetodoPagamentoID, DataID, Preco, Quantidade, Total e Imposto.

Tecnologias Utilizadas:

    Python: Linguagem de programação principal para desenvolvimento do processo ETL.
    Pandas: Utilizado para manipulação e transformação dos dados.
    SQLAlchemy: Biblioteca para a interação com o banco de dados SQL Server.
    ODBC Driver 17: Utilizado para conectar o Python ao SQL Server.
    SQL Server: Banco de dados utilizado para armazenar as tabelas dimensionais e a tabela fato.

Funcionalidades:

    Extração de dados de arquivos CSV ou DataFrame.
    Criação de tabelas dimensionais com identificadores únicos.
    Cálculo de imposto baseado em faixas de valores.
    Carregamento de dados no banco de dados SQL Server.
    Criação de tabela fato com junção das tabelas dimensionais e dados de vendas.

Como Usar:

    Conexão com o banco de dados: O banco de dados SQL Server deve estar configurado com a URL de conexão apropriada.
    Configuração dos dados: O DataFrame com os dados de vendas (df) deve estar pronto para ser utilizado.
    Execução do código: Ao executar o código, as tabelas dimensionais e a tabela fato serão criadas e carregadas no banco de dados.

Estrutura do Código:

    DimCategoria: Tabela dimensional para categorias de produtos.
    DimProduto: Tabela dimensional para produtos.
    DimMetodoPagamento: Tabela dimensional para métodos de pagamento.
    DimTempo: Tabela dimensional para tempo, baseada na data da venda.
    FatoVenda: Tabela fato contendo as transações de vendas, com referência aos IDs das tabelas dimensionais.
