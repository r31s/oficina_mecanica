# oficina_mecanica
projeto fullstack da oficina mecânica

## O que temos pra hoje:

Vamos fazer um programa em PHP para recuperar os dados dos produtos que foram cadastrados no banco de dados.

### Banco de dados utilizado
Lembrando que utilizamos a seguinte estrutura de tabela no exemplo abaixo:

```SQL
CREATE TABLE produtos (
  codigo INT AUTO_INCREMENT PRIMARY KEY,
  descricao VARCHAR(100) NOT NULL,
  unidade VARCHAR(20),
  preco DECIMAL(10,2)
);
```
> Observação: Utiiliamos o banco de dados "oficina_mecanica" para criação da tabela e execução desse exemplo.
--- 

### Programa que exibe os dados dos produtos cadastrados

Aqui está um exemplo em PHP (com HTML) que retorna os dados armazenados na tabela.

```php
<!DOCTYPE html>
<html>
	<head>
		<title>Lista de Produtos</title>
	</head>
	<body>
		<!-- Título da página -->
		<h2>Lista de Produtos</h2>
		<!-- Tabela de exibição dos produtos -->
		<table>
			<!-- Cabeçalho da tabela -->
			<thead>
				<tr>
					<th>Código</th>
					<th>Descrição</th>
					<th>Unidade</th>
					<th>Preço</th>
				</tr>
			</thead>
			<!-- Corpo da tabela -->
			<tbody>
				<?php
				// Conexão com o banco de dados
				$host = "localhost";
				$user = "root";
				$password = "";
				$database = "oficina_mecanica";

				$conexao = mysqli_connect($host, $user, $password, $database);

				// Consulta na tabela de produtos
				$sql = "SELECT * FROM produtos";
				$resultado = mysqli_query($conexao, $sql);

				// Loop para exibir os resultados
				while ($produto = mysqli_fetch_array($resultado)) {
					echo "<tr>";
					echo "<td>" . $produto['codigo'] . "</td>";
					echo "<td>" . $produto['descricao'] . "</td>";
					echo "<td>" . $produto['unidade'] . "</td>";
					echo "<td>" . $produto['preco'] . "</td>";
					echo "</tr>";
				}

				// Fechar a conexão com o banco de dados
				mysqli_close($conexao);
				?>
			</tbody>
		</table>
	</body>
</html>
```

A parte do loop para exibir os resultados é responsável por percorrer os resultados da consulta SQL realizada na tabela de produtos e mostrar cada registro em uma linha da tabela HTML que está sendo criada.

O loop começa com a função mysqli_fetch_array($resultado) que recupera um registro por vez da consulta SQL e armazena na variável $produto, que é um array associativo que contém os valores das colunas da tabela de produtos para aquele registro.

Em seguida, dentro do loop, é criada uma linha da tabela HTML, com a tag <tr>, e são adicionadas células nessa linha com as informações do registro utilizando a tag <td>. Para isso, é feito uso da função echo do PHP para escrever o código HTML na página.

O processo se repete até que não haja mais registros a serem lidos da consulta SQL.

---  
### Exemplificando com alguns dados  

Vamos supor que a tabela "produtos" no banco de dados contenha 3 registros com os seguintes valores:

| Código | Descrição         | Unidade | Preço   |
|--------|------------------|---------|---------|
| 1      | Camiseta Azul    | UN      | 29,90   |
| 2      | Calça Jeans      | UN      | 89,90   |
| 3      | Tênis Branco     | PAR     | 59,90   |
| 4      | Camisa Xadrez    | UN      | 49,90   |


```php
### Loop para exibir os resultados

while ($produto = mysqli_fetch_array($resultado)) {
    echo "<tr>";
    echo "<td>" . $produto['codigo'] . "</td>";
    echo "<td>" . $produto['descricao'] . "</td>";
    echo "<td>" . $produto['unidade'] . "</td>";
    echo "<td>" . $produto['preco'] . "</td>";
    echo "</tr>";
}
```
Ao executar o loop "while" no código fornecido, a variável $produto será preenchida com os valores dos registros da tabela "produtos". A cada iteração do loop, a variável $produto receberá um novo registro, até que todos os registros sejam percorridos.

Aqui está um exemplo de como seria a execução do loop para a tabela de produtos acima:

_Primeira iteração:_  
- $produto['codigo'] = 1  
- $produto['descricao'] = "Camiseta preta"  
- $produto['unidade'] = "un"  
- $produto['preco'] = 25.00  

_Segunda iteração:_  
- $produto['codigo'] = 2  
- $produto['descricao'] = "Calça jeans"  
- $produto['unidade'] = "un"  
- $produto['preco'] = 80.00  

_Terceira iteração:_  
- $produto['codigo'] = 3  
- $produto['descricao'] = "Tênis branco"  
- $produto['unidade'] = "par"  
- $produto['preco'] = 120.00  


---   
### Glossário  

_*tags HTML utilizadas na tabela*_  

- THEAD - Define a seção de cabeçalho de uma tabela, onde são definidos os títulos das colunas.  
- TBODY - Define a seção de corpo de uma tabela, onde são exibidos os dados.  
- TR - Define uma linha na tabela.  
- TH - Define uma célula de cabeçalho de uma tabela, geralmente usada na primeira linha da tabela para definir o título de uma coluna.  
- TD - Define uma célula de dados de uma tabela, usada para exibir os valores correspondentes a cada linha e coluna da tabela.

_*PHP (acessando banco de dados MySQL)*_  
1) mysqli_connect() - é uma função do MySQLi que é usada para criar uma nova conexão com um banco de dados MySQL. A função requer quatro parâmetros: o host (servidor onde o banco de dados está hospedado), o usuário do banco de dados, a senha do usuário e o nome do banco de dados.

2) mysqli_query() - é uma função do MySQLi que é usada para enviar uma consulta SQL ao banco de dados. A função requer dois parâmetros: a conexão do MySQLi criada pela função mysqli_connect() e a consulta SQL a ser executada.

3) mysqli_fetch_array() - é uma função do MySQLi que é usada para buscar uma linha de dados do resultado da consulta SQL e retornar um array associativo que contém os valores das colunas da tabela de banco de dados para aquele registro. A função requer um parâmetro: o resultado da consulta SQL criado pela função mysqli_query().

4) mysqli_close() - é uma função do MySQLi que é usada para fechar uma conexão com um banco de dados MySQL aberto pela função mysqli_connect(). A função requer um parâmetro: a conexão do MySQLi criada pela função mysqli_connect().  

> *Atenção* já foram construídos o formulário e a página para cadastrar os produtos na tabela de produtos.
