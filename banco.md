create database bd_paoquentinho

use bd_paoquentinho

create table perfil(
codigo					int 				primary key auto_increment,
descricao				varchar(100)		not null
)
insert into perfil(descricao) values ('caloteiro')
insert into perfil(descricao) values ('fiel')
insert into perfil(descricao) values ('infiel')
insert into perfil(descricao) values ('trabalhador')

select * from perfil

update perfil
set  descricao = 'fieles'
where codigo   =  '3'

delete from perfil where codigo = 3

create table vendedor(
 cpf					char(11)			primary key,
 nome					varchar(100)		not null,
 salario				float				not null,
 codigoPerfil			int					not null,
 foreign key (codigoPerfil)  references perfil(codigo)
)
insert into vendedor (cpf, nome, salario, codigoPerfil)  values ('89754623136', 'Bento', '1500', '1')
insert into vendedor (cpf, nome, salario, codigoPerfil)  values ('21354689725', 'Jorge', '1500', '2')
insert into vendedor (cpf, nome, salario, codigoPerfil)  values ('45687912385', 'Teco', '1500', '4')

select * from vendedor

update vendedor 
set cpf  =  '45687912385'
nome =  'jorjao'
salario =  '1500'
where codigoPerfil = '4'

delete from  vendedor where  cpf = '45687912385'

create table produto(
codigo					int					primary key auto_increment,
descricao				varchar(100)		not null,
precoKg					float				not null,
precounitariovenda		float				not null
)
insert into produto(descricao, precoKg, precounitariovenda)  values ( 'cacetinho', '3.50', '0.75')
insert into produto(descricao, precoKg, precounitariovenda)  values ( 'inpada', '10', '5')
insert into produto(descricao, precoKg, precounitariovenda)  values ( 'pão doce', '2', '0.50')

select * from produto

update produto 
set  codigo = '3'
precoKg = '2'
where precounitariovenda = '0.70'

delete from produto where codigo = '3' 

create table padeiro(
cpf						char(11)			primary key,
nome					varchar(100)		not null,
sexo					char(1)				not null,
dtnasc					datetime			not null, 
telefone				char(9)				not null,
salario					float				not null
)
insert into padeiro (cpf, nome, sexo, dtnasc, telefone, salario) values ('65498732102', 'Paulão', 'M', '1958/09/24', '996633225', '1900')
insert into padeiro (cpf, nome, sexo, dtnasc, telefone, salario) values ('21354689725', 'Maria', 'F', '2004/06/13', '774411228', '1900')
insert into padeiro (cpf, nome, sexo, dtnasc, telefone, salario) values ('98765432196', 'Chico', 'M', '1899/05/03', '336699887', '1900')

select * from padeiro  

update cpf =  '98765432196'
nome = 'Chicao'
sexo = 'M'
dtnasc = '1899/05/03'
telefone = '336699887'
where salario = '1900'

delete from padeiro where cpf =   '98765432196' 

create table vende (
qtd						float				not null,
preco					float				not null,
dthr					datetime			not null default current_timestamp(),
cpfVendedor				char(11)			not null,
codigoProduto			int					not null,
primary key (cpfVendedor, codigoProduto, dthr),
foreign key (cpfVendedor)	references vendedor(cpf),
foreign key (codigoProduto) references produto(codigo)	
)
insert into vende(qtd, preco, dthr, cpfVendedor, codigoProduto) values ('608', '3.50', '20/03/2023', '89754623136', '1')
insert into vende(qtd, preco, dthr, cpfVendedor, codigoProduto) values ('950', '4.50', '21/03/2023', '21354689725', '2')
insert into vende(qtd, preco, dthr, cpfVendedor, codigoProduto) values ('650', '4.50', '22/03/2023', '89754623136', '3')

select * from vende =  '650'

update qtd = '650'
set preco = '3.55'
dthr = '22/03/2023'
cpfVendedor = '89754623136'
where codigoProduto = '3'

delete from vende where qtd = '650'
 

create table produz (
qtd						float			 	not null,
dt						datetime			not null,
precokg					float				not null,
cpfPadeiro				char(11)			not null,
codigoProduto			int					not null,
primary key (cpfPadeiro, codigoProduto, dt),
foreign key (cpfPadeiro) references padeiro(cpf),
foreign key (codigoProduto) references produto(codigo)							
)
insert into produz(qtd, dt, precokg, cpfPadeiro, codigoProduto) values ('190', '20/03/2022', '7.50', '32165498785', '1')
insert into produz(qtd, dt, precokg, cpfPadeiro, codigoProduto) values ('130', '19/03/2022', '8.50', '32165498785', '2')
insert into produz(qtd, dt, precokg, cpfPadeiro, codigoProduto) values ('520', '18/0', '9.50', '98765432196', '3')

select * from produz

update qtd = '520'
set dt = '18/03/2022'
precokg = '9.50'
cpfPadeiro = '98765432196'
where codigoProduto = '3'


delete  from produz where qtd = '520'  