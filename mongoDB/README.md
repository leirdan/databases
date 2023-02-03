# 1. INTRODUÇÃO AO MONGODB

O MongoDB é um SGBD (Sistema Gerencial de Banco de Dados) do tipo NoSQL - ou seja, é não-relacional e não utiliza comandos do tipo SQL (como os do PostgreSQL, MySQL e outros). O MongoDB funciona da seguinte forma:

-   Cada "tabela" é chamada de **Collection** (coleção);
-   Cada conjunto de dados inserido numa Collection é chamado de **Document** (documento) e, muitas vezes, têm estruturas do tipo JSON;

    -   A estrutura de documentos permite que existam, dentro de um documento, outros documentos aninhados;
    -   Por exemplo:

    ```json
    {
    	"title": "mother tongue",
    	"year": 2019,
    	"genre": "pop rock",
    	"band": {
    		"name": "bring me the horizon",
    		"members": "...."
    	}
    }
    ```

    -   Neste caso, em uma Collection de "Songs" o seguinte documento detalhando uma música tem outro documento dentro de si, que detalha a banda que a compôs e tem propriedades próprias.

Dessa forma, as consultas de dados podem ser mais fáceis a depender do caso. O MongoDB também é um banco de dados bastante rápido.
