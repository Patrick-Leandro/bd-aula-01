# bd-aula-01

Exercicio 01
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
