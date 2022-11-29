-- DDL - LINGUAGEM DE DEFINICAO DE DADOS
CREATE DATABASE RpgBE10

USE RpgBE10

CREATE TABLE Usuarios(
	IdUsuario INT PRIMARY KEY IDENTITY,
	Email VARCHAR(100) UNIQUE NOT NULL,
	Senha VARCHAR(255) NOT NULL
)

CREATE TABLE Classes(
	IdClasse INT PRIMARY KEY IDENTITY,
	Nome VARCHAR(50) UNIQUE NOT NULL,
	Descricao VARCHAR(250) NOT NULL
)

CREATE TABLE Personagens(
	IdPersonagem INT PRIMARY KEY IDENTITY,
	Nome VARCHAR(30) UNIQUE NOT NULL,
	IdUsuario INT UNIQUE FOREIGN KEY REFERENCES Usuarios(IdUsuario),
	IdClasse INT UNIQUE FOREIGN KEY REFERENCES Classes(IdClasse)
)

CREATE TABLE Habilidades(
	IdHabilidade INT PRIMARY KEY IDENTITY,
	Nome VARCHAR(50) UNIQUE NOT NULL,
	Descricao VARCHAR(255) NOT NULL,
)

CREATE TABLE ClassesHabilidades(
	IdHabilidade INT FOREIGN KEY REFERENCES Habilidades(IdHabilidade),
	IdClasse INT FOREIGN KEY REFERENCES Classes(IdClasse)
)

-- DML - LINGUAGEM DE MANIPULACAO DE DADOS

INSERT INTO Classes VALUES 
	('Mago', 'Lança feitiços'),
	('Bárbaro', 'Ataque forte'),
	('Monge', 'Curandeiro')

INSERT INTO Habilidades VALUES
	('Lança Mortal', 'Gira a lança contra o vento'),
	('Recuperar Vida', 'Recupera 50 de vida'),
	('Bola de Fogo', 'Cria uma bolo de fogo no ar'),
	('Escudo Supremo', 'Defende de qualquer coisa'),
	('Corrida Lenta', 'Desvia de uma habilidade rapida')

INSERT INTO ClassesHabilidades VALUES
	--Mago
	(1,3), (1,4),
	--Barbaro
	(2,1), (2,4), (2,5),
	--Monge
	(3,2), (3,4), (3,5)

INSERT INTO Usuarios VALUES
	--Aphonso
	('usuario1@email.com', '123123'),
	--Danox
	('usuario2@email.com', '321321')

INSERT INTO Personagens VALUES
	('DeuBug', 1, 2),
	('BitBug', 2, 3)

INSERT INTO Usuarios VALUES
	('vaiserdeletado@deletar.com', '123321')

DELETE FROM Usuarios WHERE Email = 'vaiserdeletado@deletar.com'

UPDATE Usuarios SET Email = 'aphonsousuario1@email.com' WHERE IdUsuario = 1
UPDATE Usuarios SET Email = 'danoxusuario2@email.com' WHERE IdUsuario = 2

SELECT * FROM Usuarios WHERE IdUsuario = 2

--DQL - Consultas
SELECT * FROM Usuarios
SELECT * FROM Classes
SELECT * FROM Personagens
SELECT * FROM Habilidades
SELECT * FROM ClassesHabilidades

SELECT Nome FROM Classes
SELECT Nome, Descricao FROM Classes
SELECT Nome, Descricao FROM Classes WHERE IdClasse = 2

SELECT Personagens.Nome, Classes.Nome
FROM Personagens
INNER JOIN Classes
ON Personagens.IdClasse = Classes.IdClasse

--DCL - CONTROLE

CREATE LOGIN aphonso WITH PASSWORD = '1234'
CREATE USER aphonso FOR LOGIN aphonso

GRANT SELECT TO aphonso 
