## SQL - Dia 1

Projeção - É escolher as colunas.
Seleção - É a escolha de linhas.
Join - A união de dados em tabeals diferentes.

- Comandos

![SQL_Comandos](SQL_Comandos.png)

- Juntando colunas

![Concatenando](Concatenando_colunas.png)

- Clasulas Where

![Clasulas Where](Where.png)

- No caso abaixo o certo seria usar o Having

![Having](Having.png)

- Case é util quando queremos ja converter valores para outro tipo.

![Case](Case.png)

Por exemplo, digamos que tem sexo 1 e 2, mas o 1 é masculino e o 2 feminito.

Podemos fazer:

Select nome, CASE sexo WHEN '1' THAN 'm'
ELSE 'f'
END