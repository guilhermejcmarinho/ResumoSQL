# SQL

## Modelo Entidade Relacionamento - MER

Quando trabalhamos com o MER devemos nos atentar a alguns pontos como:
- Nome das entidades sempre em minúsculo, escolhendo entre singular ou plural
- Sempre manter um padrão para a nomeção de chaves secundárias. Ex: fk_tabela_1
- Evitar usar chaves primárias que não sejam geradas pelo banco, pois existe possibilidade de erro de digitação por parte do usuário.
## Normalização de dados

#### 1ª Forma Normal (1FN)
Consiste em garantir que todas as entidades estejam com campos atômicos, ou seja, sem serem multivalorados.

Por exemplo, endereço estar bem dividido, ou caso exista mais de um telefone garantir que cada um terá sua coluna.

#### 2ª Forma Normal (2FN)
Consiste em garantir que todos os atributos não chave sejam dependes do atributo chave. Se necessário dividir em 2 ou mais tabelas.

#### 3ª Forma Normal (3FN)
Nessa Forma Normal deve-se excluir colunas que podem ser obtidas por meio de operações entre outras colunas.

Por exemplo, caso tenhamos uma coluna de "valor unitário" e outra de "quantidade", não precisamos ter uma com "valor total", pois podemos obter a mesma multiplicando as duas anteriores.

#### Outras Formas Normais
Existem ao todo 5 Formas Normais, porém o uso da 4FN e 5 FN são bem incomuns e por isso a base de dados já é considerada normalizada ao chegar na 3FN.

## Comandos SQL
Abaixo temos um quadro com os principais comando quando trabalhamos com SQL:
![SQL_Comandos](Imagens/SQL_Comandos.png)

### DCL - Data Control Language
Aqui temos um subgrupo para aspectos de autorização de acesso aos dados e licenças de usuários.

- __GRANT__: Autoriza o usuário a executar operações no banco.

Ex: GRANT SELECT ON tabela TO pessoa;
- __REVOKE__: Tira as permissões cedidas do usuário.

Ex: REVOKE CREATE TABLE FROM pessoa;

### DTL - Data Transaction Language
Subgrupo que serve para controle de versionamento e afins.

- __BEGIN__: Inicia a transação
- __COMMIT__: Finaliza a transação
- __ROLLBACK__: Desfaz alterações depois do último COMMIT.

### DDL - Data Definition Language
Subgrupo que cria, altera e exclui banco de dados, tabelas e itens de índice.

- __CREATE__: Utilizado para criação de bancos, tabelas, etc

Ex: CREATE DATABASE banco;
- __ALTER__:Faz a alteração em tabelas

Ex: ALTER TABLE cliente ADD telefone VARCHAR(14);
- __DROP__: Serve para deletar bancos e tabelas

Ex: DROP TABLE cliente;

### DML - Data Manipulation Language
Subgrupo de insersão, alteração e deleção de registros na tabela.

- __INSERT__: Serve para adicionar registro em uma tabela.

Ex: INSERT INTO cliente(nome, telefone) VALUES ('José', '1234-5678')
- __UPDATE__: Altera um registro na tabela com base na chave primária.

Ex: UPDATE cliente SET nome='Maria' WHERE idcliente = 1;
- __DELETE__: Exclui um registro na tabela com base na chave primária.

Ex: DELETE FROM cliente WHERE idcliente = 1;

### DQL - Data Query Language
Subgrupo de consulta SQL, sendo o mais utilizado. Aqui temos apenas o comando __SELECT__, que é o responsavel tanto pelas consultas mais simples quanto as mais complexas.

Ex: SELECT * FROM clientes;

Quando queremos aplicar um filtro no nosso SELECT utilizamos a cláusula WHERE. Esse por sua vez pode ser utilizado com as estruturas: >, <, =>, =<, <>, =, IN, BETWEEN..AND.., LIKE, AND, OR, NOT

## Funções de agregação
As funções de agregação servem para pegar informações de resultados únicos em uma coluna. Um exemplo disso seria: maior salário em uma empresa, quantidade de clientes, etc.

Algumas dessas funções são:

- __MAX(coluna)__: Retorna o maior valor da coluna
- __MIN(coluna)__: Retorna o menor valor da coluna
- __SUM(coluna)__: Retorna a soma da coluna
- __AVG(coluna)__: Retorna a média da coluna
- __ROUND(coluna,__ casas_decimais): Arredonda o número com base na última casa decimal. 
- __TRUNC(coluna, casas_decimais)__: Arredonda o número fixando valor da casa decimal selecionada.
- __COUNT(*)__: Geralmente utilizado para saber a contagem de registros. Essa contagem ignora linhas _null_
- __SUBSTR(coluna, posicao_inicial, nº_caracteres)__: Mostra uma quantidade X de caracteres a partir da _posicao_inicial_;

__OBS¹:__ Se ao usar uma dessas funções, ela não estiver sozinha no SELECT, será necessário utilizar um GROUP BY em outro elemento da consulta.

__OBS²:__ Caso seja necessário aplicar um filtro nas funções de agregação, utilizamos o comando HAVING, que possui a mesma função do WHERE.

Ex: SELECT departamento, SUM(salario) GROUP BY departamento HAVING SUM(salario) >= 1000;

## Funções de agrupamento e ordenação

### GROUP BY
O GROUP BY é utillizado para agrupar elementos de um mesmo tipo. Um exemplo prático e fácil de imaginar é agrupamento por ano.

Ex: SELECT ano, loja, faturamento FROM vendas GROUP BY ano;

### ORDER BY
Esse comando faz a ordenação dos dados em ordem crescente ou descresente. Quando não específicado o padrão é crescente.

Ex: SELECT * FROM vendas ORDER BY loja;

## Funções de Data/Hora
Essas funções são nativas do SQL e servem para facilitar o desenvolvimento. São funções que funcionam mesmo sem uma base de dados.

- __Curdate()__: retorna data atual no formato (aaaa-mm-dd)
- __Curtime()__: retorna a hora atual no formato (hh:mm:ss)
- __Date_add(data, intervalo)__: adiciona um intervalo de dias/horas/anos/etc a data passada inicialmente.
- __Date_sub(data, intervalo)__: subtrai um intervalo de dias/horas/anos/etc a data passada inicialmente.
- __DateDiff(expressão1, expressão2)__: calcula a diferença entre duas datas.
- __DateFormat(data, formato)__: altera a formatação apresentada da data. Ex: SELECT date_format(Curdate(), '%d/%m/%a')
- __DayName(data)__: retorna o nome do dia da semana.

OBS: Para retornar o nome em português colocar antes do select o comando: _SET lc_time_names = 'pt-BR';_
- __DayofMonth(data)__: retorna apenas o dia do mês
- __From_Days(n)__: retorna a data após N dias
- __Now()__: retorna data e hora atual
- __Time()__: retorna apenas a hh:mm:ss de um dado
- __Sec_to_time(segundos)__: converte segundos em horas 
- __Time_to_sec(hora)__: converte horas em segundos  
- __Hour/Minute/Second(hora)__: Retorna apenas a HH ou MM ou SS de um dado
Ex: SELECT HOUR(14:15:16), MINUTE(14:45:18), SECOND(14:15:16) -> Retornaria 14, 45 ou 18

## JOINS

Joins são recursos que permitem acessar dados de diferentes tabelas. Os mais importantes são:

- __Produto Cartesiano__: Uma junção de produto cartesiano é uma junção entre duas tabelas que origina uma terceira tabela constituída por todos os elementos da primeira combinadas com todos os elementos da segunda.
```
SELECT c.id, c.nome, c.data_nascimento, c.telefone, p.cargo
FROM clientes AS c, pedidos AS p
WHERE c.id_profissao = p.id;
```
- __Inner Join__: Uma junção interna é caracterizada por uma consulta que retorna apenas os dados que atendem às condições de junção, isto é, quais linhas de uma tabela se relacionam com as linhas de outras tabelas. Para isso utilizamos a cláusula ON, que é semelhante à cláusula WHERE.
```
SELECT c.id, c.nome, c.data_nascimento, c.telefone, p.cargo
FROM clientes AS c INNER JOIN pedidos AS p
ON c.id_profissao = p.id;
```
- __Outer Join__: Uma junção externa é uma consulta que não requer que os registros de uma tabela possuam registros equivalentes em outra. 
Este tipo de junção se subdivide dependendo da tabela do qual admitiremos os registros que não possuem correspondência: a tabela da esquerda, a direita ou ambas.

    - __Left Outer Join__: O resultado desta consulta sempre contém todos os registros da tabela esquerda (ou seja, a primeira tabela mencionada na consulta), mesmo quando não exista registros correspondentes na tabela direira. 
    Desta forma, esta consulta retorna todos os valores da tabela esquerda com os valores da tabela direita correspondente, ou quando não há correspondência retorna um valor NULL.
    ```
    SELECT * FROM clientes
    LEFT OUTER JOIN pedidos
    ON clientes.id_pedido = pedidos.id;
    ```
    - __Right Outer Join__: Esta consulta é inversa à anterior e retorna sempre todos os registros da tabela à direita (a segunda tabela mencionada na consulta), mesmo se não existir registro correspondente na tabela à esquerda. 
    Nestes casos, o valor NULL é retornado quando não há correspondência.
    ```
    SELECT * FROM clientes
    RIGHT OUTER JOIN pedidos
    ON clientes.id_pedido = pedidos.id;
    ```

    - __Full Outer Join__: Esta consulta traz então os dados de ambas tabelas de acordo com suas correspondências e
    caso não tenha preenche o valor com NULL.
    ```
    SELECT * FROM clientes
    FULL OUTER JOIN pedidos
    ON clientes.id_pedido = pedidos.id;
    ```

![Joins Resultados](Imagens/Joins_Resultado.png)

Sendo assim em resumo temos:

__Junção de produto cartesiano__ é uma junção entre duas tabelas que origina uma terceira tabela constituída por todos os elementos da primeira tabela combinada com todos os elementos da segunda.

__Junção Interna (Inner Join)__ todas as linhas de uma tabela se relacionam com todas as linhas de outras tabelas se elas tiverem ao menos 1 campo em comum. 

__Junção Externa Esquerda (Left Outer Join)__ traz todos os registros da tabela esqueda mesmo quando não exista registros correspondentes na tabela direita. 

__Junção Externa Direita (Right Outer Join)__ traz todos os registros da tabela direita mesmo quando não exista registros correspondentes na tabela esquerda. 

__Junção Externa Completa (Full Outer Join)__ apresenta todos os dados das tabelas à esquerda e à direita, mesmo que não possuam correspondência em outra tabela.

![Joins](Imagens/SQL_Joins.jpeg)

## Subconsultas

Uma subconsulta nada mais é do que uma instrução SELECT dentro de outro SELECT que retorna algumas colunas específicas. Uma subconsulta SQL é chamada de consulta interna, enquanto a consulta que contém a subconsulta é chamada de consulta externa.

Vale lembrar que a consulta interna (subconsulta), é executada primeiro e retorna um conjunto de resultados, esses resultados serão usados na próxima consulta.

- Exemplo 1
```
SELECT nome, sobrenome
FROM funcionarios
WHERE id_escritorio IN (SELECT id FROM escritorios WHERE pais = 'Brasil');
```
No exemplo acima, estamos selecionando os campos 'nome' e 'sobrenome' da tabela de funcionário onde o id do escritório esteja dentro do resultado da subconsulta.

- Exemplo 2
```
SELECT f.nome, f.sobrenome, e.pais, p.salario
FROM pagamentos AS p, funcionarios AS f, escritorios AS e
WHERE f.id_escritorio = e.id
AND f.id = p.id_funcionario
AND salario = (SELECT MAX(salario) FROM pagamentos)
```

No exemplo acima, estamos efetuando uma junção de tabela por produto cartesiano, utilizando uma função agregada e uma subconsulta para ver quem tem o mair salário na empresa.

- Exemplo 3
```
SELECT f.nome, f.sobrenome, e.pais, p.salario
FROM pagamentos AS p, funcionarios AS f, escritorios AS e
WHERE f.id_escritorio = e.id
AND f.id = p.id_funcionario
AND salario < (SELECT AVG(salario) FROM pagamentos)
```
No exemplo acima, estamos efetuando uma junção de tabela por produto cartesiano, utilizando uma função agregada e uma subconsulta para ver quem recebe menos que a média salarial da empresa.
