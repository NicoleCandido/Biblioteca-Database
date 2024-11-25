# Biblioteca-Database
Este é um exemplo de um banco de dados para gerenciamento de uma biblioteca.
Biblioteca.sql
CREATE SCHEMA IF NOT EXISTS Biblio DEFAULT CHARACTER SET utf8;
use Biblio;
create table Livro(
id int not null primary key auto_increment,
titulo varchar (100) not null) engine = InnoDB;
select * from Livro;

create table Usuario(
id int not null primary key auto_increment,
nome varchar (100) not null,
email varchar (250),
data_de_nascimento date,
quantidade_emprestimo int not null default 0) engine = InnoDB;
select * from Usuario;

create table Emprestimo(
id int not null primary key auto_increment,
Usuario_id int not null,
Livro_id int not null,
data_de_emprestimo date,
data_de_devolucao date,
data_de_entregao date,
foreign key (Usuario_id) references Usuario(id),
foreign key (Livro_id) references Livro(id)
) engine = InnoDB;
select * from Emprestimo;

INSERT INTO Livro (titulo) VALUES ("Bagagem"),
("O Cortiço"),
("Lira dos vinte anos"),
("Quarup"),
("O tronco"),
("A escrava Isaura"),
("O pagador de promessas"),
("O que é isso, companheiro"),
("Vidas secas"),
("Grande sertão varedas");


INSERT INTO Usuario (nome,email,data_de_nascimento) VALUES 
("João Silva", "joao@gmail.com","1992-08-09"),
("Maria Mota","maria@gmail.com","1984-05-07"),
("Eduardo Caçando","eduardo@gmail.com","1996-02-23"),
("Silvia Alencar","silvia@gmail.com","1973-09-20"),
("Gabriela Medeiros","gabriela@gmail.com","1993-01-10"),
("Karina Silva","Karina@gmail.com","1995-03-25");

INSERT INTO Emprestimo (Usuario_id, Livro_id,data_de_emprestimo,data_de_devolucao,data_de_entregao) VALUES 
(1,4,"2014-07-15","2014-08-15","2014-08-10"),
(3,2,"2014-08-22","2014-09-22","2014-09-21"),
(2,6,"2014-08-22","2014-09-22",null),
(2,8,"2014-09-21","2014-10-21",null),
(1,10,"2014-09-23","2014-10-23","2014-09-29"),
(4,2,"2014-09-23","2014-10-23",null),
(4,7,"2014-09-23","2014-10-23",null),
(5,3,"2014-09-24","2014-10-24",null),
(5,9,"2014-09-24","2014-10-24",null),
(5,1,"2014-09-24","2014-10-24",null),
(6,3,"2014-09-01","2014-10-01","2014-09-30");

set @data_de_emprestimo = curdate();
set @data_de_devolucao = adddate(@data_de_emprestimo, interval 30 day);

insert into Emprestimo (Usuario_id, Livro_id,data_de_emprestimo,data_de_devolucao) values
(1,5,@data_de_emprestimo,@data_de_devolucao);

select *from Emprestimo;
