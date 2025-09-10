REPOSITORIO com apenas o docker-compose com banco postgre para fazer o exercicio no pgadmin:

*Lista de exercícios de banco de dados:*

* Abra o MySQL Workbench e crie um banco de dados chamado 'exercicio01'
create database exercicio01;
use exercicio01;

* Crie uma tabela chamada tipo conforme abaixo:
	create table tipo(
		id	int		primary key,
		nome	varchar(25)	not null);

* Insira os seguintes registros na tabela de tipo:
	insert into tipo(id, nome) values(1, 'Eletrônicos');
	insert into tipo(id, nome) values(2, 'Livraria');
	insert into tipo(id, nome) values(3, 'Informática');
	insert into tipo(id, nome) values(4, 'Games');
	insert into tipo(id, nome) values(5, 'Vestuário');

  *** Faça as seguintes consultas:
 
    
	* Exiba o id e o nome dos tipos em ordem alfabética
* R: 	select id, nome from tipo order by nome

	
	* Exiba o id e o nome dos tipos que começam com a letra "E"
* R:  select id, nome from tipo where nome like 'E%'
	
	* Exiba o id e o nome dos tipos que começam com a letra "E" ou com a letra "I"
* R:  select id, nome from tipo where nome like 'E%' or nome like 'I%'
	
	* Exiba o id e o nome dos tipos que possuem id maior ou igual a 3
* R: select  id, nome from tipo where id>=3

  
---

* Crie uma tabela chamada produto conforme abaixo:
create table produto (
    id          serial primary key,
    nome        varchar(25) not null,
    preco       numeric(10,2) not null,
    quantidade  int not null,
    tipo_id     int not null,
    foreign key (tipo_id) references tipo(id)
);


* Cadastre os produtos abaixo:

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (1, 'Smartphone', 2500.00, 15, 1);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (2, 'TV 50 Polegadas', 3200.00, 8, 1);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (3, 'Livro Java', 120.00, 30, 2);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (4, 'Livro Angular', 150.00, 20, 2);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (5, 'Notebook', 4800.00, 12, 3);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (6, 'Mouse Gamer', 180.00, 40, 3);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (7, 'Console PS5', 4500.00, 5, 4);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (8, 'Jogo FIFA 25', 350.00, 25, 4);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (9, 'Camiseta Polo', 80.00, 50, 5);

		insert into produto(id, nome, preco, quantidade, tipo_id) 
		values (10, 'Tênis Nike', 400.00, 20, 5);

* Faça consultas para:

	* Exibir o id, nome, preco, quantidade dos produtos ordenando em ordem alfabética
* R: select id, nome, preco, quantidade from produto order by nome;

	
	* Exibir o id, nome, preco, quantidade dos produtos cujo nome começa com a letra 'C'
* R: select id, nome, preco, quantidade from produto where nome like 'C%';
	
	* Exibir o id, nome, preco, quantidade dos produtos cujo preço é maior do que 100 
* R: select id, nome, preco, quantidade from produto where preco>100;
	
	* Exibir o id, nome, preco, quantidade dos produtos cujo preço está entre 100 e 1000 e em ordem crescente de preço
* R: select id, nome, preco, quantidade from produto where preco>100 and preco<1000 order by preco asc;
	
	* Exibir o id, nome, preco, quantidade dos produtos cujo nome começa com a letra 'C' e o preço está entre 100 e 5000
* R: select id, nome, preco, quantidade from produto where nome like 'C%' and preco>=100 and preco<=5000;

---

FIZ COM GPT NAO CONSEGUI

 * Exibir o id do produto, nome do produto, preco, quantidade, id do tipo e nome do tipo em ordem alfabética do nome do produto
* R: select 
    p.id as id_produto,
    p.nome as nome_produto,
    p.preco,
    p.quantidade,
    t.id as id_tipo,
    t.nome as nome_tipo
from produto p
join tipo t on p.tipo_id = t.id
order by p.nome asc;

	 
	* Exibir o id do produto, nome do produto, preco, quantidade, id do tipo e nome do tipo somente para tipo = 'Informática'
* R: select 
    p.id as id_produto,
    p.nome as nome_produto,
    p.preco,
    p.quantidade,
    t.id as id_tipo,
    t.nome as nome_tipo
from produto p
join tipo t on p.tipo_id = t.id
where t.nome = 'Informática'
order by p.nome;

	   
	* Faça uma consulta que retorne o nome do tipo e a quantidade de produtos de cada tipo
*  R:select 
    t.nome as nome_tipo,
    count(p.id) as quantidade_produtos
from tipo t
left join produto p on p.tipo_id = t.id
group by t.nome
order by t.nome;

     
	* Faça uma consulta que retorne o nome do tipo e o somatório do preço dos produtos de cada tipo
*  R: select 
    t.nome as nome_tipo,
    sum(p.preco) as soma_precos
from tipo t
left join produto p on p.tipo_id = t.id
group by t.nome
order by t.nome;





