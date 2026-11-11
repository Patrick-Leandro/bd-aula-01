# bd-aula-01

Exercicio 01  Uma loja que vende equipamento de informática. O banco de dados deve ter as tabelas: cliente, produto e pedido.


DROP DATABASE IF EXISTS loja_informatica_db;
CREATE DATABASE loja_informatica_db;
USE loja_informatica_db;

-- Cliente
CREATE TABLE cliente (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    telefone VARCHAR(20)
);

-- Produto
CREATE TABLE produto (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    marca VARCHAR(50),
    preco DECIMAL(10,2) NOT NULL,
    estoque INT NOT NULL
);

-- Pedido
CREATE TABLE pedido (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT,
    data_pedido DATE NOT NULL,
    valor_total DECIMAL(10,2),

    FOREIGN KEY (id_cliente)
    REFERENCES cliente(id)
    ON DELETE CASCADE
);

-- Itens do pedido
CREATE TABLE item_pedido (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_pedido INT,
    id_produto INT,
    quantidade INT NOT NULL,

    FOREIGN KEY (id_pedido)
    REFERENCES pedido(id)
    ON DELETE CASCADE,

    FOREIGN KEY (id_produto)
    REFERENCES produto(id)
    ON DELETE CASCADE
);

-- Dados de teste

INSERT INTO cliente (nome,email,telefone) VALUES
('João Silva','joao@email.com','31999999999'),
('Maria Souza','maria@email.com','31888888888');

INSERT INTO produto (nome,marca,preco,estoque) VALUES
('Notebook Dell','Dell',4500.00,10),
('Mouse Gamer','Logitech',150.00,30),
('Monitor 24 Pol','LG',850.00,15);

INSERT INTO pedido (id_cliente,data_pedido,valor_total) VALUES
(1,'2026-05-10',4650.00);

INSERT INTO item_pedido (id_pedido,id_produto,quantidade) VALUES
(1,1,1),
(1,2,1);

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Exercicio 02: Um site de viagens. O banco de dados deve ter as tabelas: cliente, destino turístico e pacote de viagem.

DROP DATABASE IF EXISTS viagens_db;
CREATE DATABASE viagens_db;
USE viagens_db;

-- Cliente
CREATE TABLE cliente (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL
);

-- Destino Turístico
CREATE TABLE destino (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    pais VARCHAR(100) NOT NULL,
    descricao TEXT
);

-- Pacote de Viagem
CREATE TABLE pacote_viagem (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_cliente INT,
    id_destino INT,
    data_viagem DATE NOT NULL,
    valor DECIMAL(10,2) NOT NULL,

    FOREIGN KEY (id_cliente)
    REFERENCES cliente(id)
    ON DELETE CASCADE,

    FOREIGN KEY (id_destino)
    REFERENCES destino(id)
    ON DELETE CASCADE
);

-- Dados de teste

INSERT INTO cliente (nome,email) VALUES
('Ana Costa','ana@email.com'),
('Carlos Lima','carlos@email.com');

INSERT INTO destino (nome,pais,descricao) VALUES
('Paris','França','Cidade Luz'),
('Cancún','México','Praias paradisíacas'),
('Roma','Itália','Cidade histórica');

INSERT INTO pacote_viagem (id_cliente,id_destino,data_viagem,valor) VALUES
(1,1,'2026-07-15',7500.00),
(2,2,'2026-08-10',5200.00);

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Exercício 03: Gerenciar o estoque de produtos de uma empresa em cada uma de suas filiais.

DROP DATABASE IF EXISTS estoque_filiais_db;
CREATE DATABASE estoque_filiais_db;
USE estoque_filiais_db;

-- Produto
CREATE TABLE produto (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    categoria VARCHAR(50),
    preco DECIMAL(10,2)
);

-- Filial
CREATE TABLE filial (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    cidade VARCHAR(100)
);

-- Estoque por filial
CREATE TABLE estoque (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_produto INT,
    id_filial INT,
    quantidade INT NOT NULL,

    FOREIGN KEY (id_produto)
    REFERENCES produto(id)
    ON DELETE CASCADE,

    FOREIGN KEY (id_filial)
    REFERENCES filial(id)
    ON DELETE CASCADE
);

-- Dados de teste

INSERT INTO produto (nome,categoria,preco) VALUES
('Teclado Mecânico','Periféricos',250.00),
('Monitor 27','Monitores',1200.00),
('SSD 1TB','Armazenamento',450.00);

INSERT INTO filial (nome,cidade) VALUES
('Filial Centro','Belo Horizonte'),
('Filial Norte','Contagem'),
('Filial Sul','Betim');

INSERT INTO estoque (id_produto,id_filial,quantidade) VALUES
(1,1,20),
(1,2,15),
(2,1,10),
(2,3,12),
(3,2,25);


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

