📌 Sistema de Gerenciamento de Estacionamento

Este projeto descreve um sistema de gerenciamento de estacionamentos, abrangendo os modelos conceitual, lógico e físico do banco de dados. O objetivo é estruturar de forma clara como Motoristas, Estacionamentos e Vagas se relacionam.

📘 1. Modelo Conceitual (DER)

O Modelo Conceitual representa, de forma abstrata, as entidades e seus relacionamentos.

Entidades
🧍 Motorista

ID_motorista (PK)

nome

telefone

🅿️ Estacionamento

ID_estacionamento (PK)

nome

endereço

🚗 Vaga

ID_vaga (PK)

número

estado (ocupada, livre, reservada)

Relacionamentos
🔹 Motorista — Estacionamento

1 Motorista gerencia N Estacionamentos

Relacionamento 1:N

🔹 Estacionamento — Vaga

1 Estacionamento possui N Vagas

Relacionamento 1:N

📗 2. Modelo Lógico

O Modelo Lógico representa o banco com mais detalhes estruturais, incluindo chaves estrangeiras e cardinalidade.

Tabela: Motorista
Campo	Tipo	Chave
ID_motorista	INT	PK
nome	VARCHAR	
telefone	VARCHAR	
Tabela: Estacionamento
Campo	Tipo	Chave
ID_estacionamento	INT	PK
nome	VARCHAR	
endereço	VARCHAR	
ID_motorista	INT	FK → Motorista(ID_motorista)

📌 Representa que cada estacionamento é gerenciado por um único motorista.

Tabela: Vaga
Campo	Tipo	Chave
ID_vaga	INT	PK
número	INT	
estado	VARCHAR	
ID_estacionamento	INT	FK → Estacionamento(ID_estacionamento)

📌 Uma vaga pertence a apenas um estacionamento.

📙 3. Modelo Físico (SQL)

Abaixo está a implementação em SQL para criação das tabelas:

CREATE TABLE Motorista (
    ID_motorista INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20)
);

CREATE TABLE Estacionamento (
    ID_estacionamento INT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    endereco VARCHAR(200),
    ID_motorista INT NOT NULL,
    FOREIGN KEY (ID_motorista) REFERENCES Motorista(ID_motorista)
);

CREATE TABLE Vaga (
    ID_vaga INT PRIMARY KEY,
    numero INT NOT NULL,
    estado VARCHAR(20) CHECK (estado IN ('ocupada', 'livre', 'reservada')),
    ID_estacionamento INT NOT NULL,
    FOREIGN KEY (ID_estacionamento) REFERENCES Estacionamento(ID_estacionamento)
);

✅ Resumo do Sistema

1 Motorista gerencia N Estacionamentos

1 Estacionamento possui N Vagas

Estrutura simples e eficiente para controle de vagas e gestores

Modelo ideal para sistemas de controle de estacionamentos comerciais
