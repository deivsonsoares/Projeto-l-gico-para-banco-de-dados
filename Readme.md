#criação do banco de dados para o cenário de E-commerce
create database ecommerce;
use ecommerce;

#criar tabela cliente
create table clients(
	idClient int auto_increment primary key,
    Fname varchar(10),
    Minit char(3),
    Lname varchar(20),
    CPF char(11) not null,
    Address varchar(30),
    #criado constraint para cpf
    constraint unique_cpf_client unique (CPF)
);

alter table Clients auto_increment=1;
#criar tabela produto
create table product(
	idproduct int auto_increment primary key,
    Pname varchar(10) not null,
    classification_kids bool  default false,
    category enum('Eletrônico','Vestimenta','Alimentos','Móveis') not null,
    avaliation float  default 0,
    size varchar(10)
);
#criar tabela pagamento
#create table payments(
#idClient int,
#id_payment int,
#typePayment enum('Boleto','Cartão','Dois cartões'),
#limitAvailable float,
#dateValid float,
#primary key(idClient,id_payment)
#);

#criar tabela pedido

create table orders(
	idOrder int auto_increment primary key,
    idOrderClient int,
	orderStatus enum('Cancelado','Confirmado','Em Processamento') default 'Em processamento',
    orderDescripiton varchar(255),
    sendValue float default 10,
    paymentCash bool default false,
    #criado constraint para cpf
    constraint fk_orders_client foreign key (idOrderClient) references clients(idclient)
);
#criar tabela estoque

create table productStorage(
	idProdStorage int auto_increment primary key,
    storageLocation varchar(255),
    quantify int default 0
);
#criar tabela fornecedor
create table supplier(
	idSupplier int auto_increment primary key,
    socialName varchar(255) not null,
    CNPJ char(15) not null,
    contat varchar(11) not null,
    #constraint cnpj unique
    constraint unique_supplier unique (CNPJ)
);

#criar tabela vendedor

create table seller(
	idSeller int auto_increment primary key,
    socialName varchar(255) not null,
    AbstName varchar(255),
    CNPJ char(15),
    CPF char(9),
    location varchar(255),
    contat varchar(11) not null,
    #constraint cnpj unique
    constraint unique_cnpj_seller unique (CNPJ),
    constraint unique_cpf_seller unique (CPF)
);
# criar tabela produtos_vendedor
create table productSeller(
idPseller int,
idPproduct int,
prodQuantity int default 1,
primary key (idPseller, idPproduct),
constraint fk_product_seller foreign key (idPseller) references seller(idSeller),
constraint fk_product_product foreign key (idPproduct) references product(idProduct)
);

create table productOrder(
	idPOproduct int,
    idPOorder int,
    poQuantity int default 1,
    poStatus enum('Disponível','Sem estoque') default 'Disponível',
    primary key (idPOproduct, idPOorder),
    constraint fk_productorder_seller foreign key(idPOproduct) references product(idProduct),
    constraint fk_productorder_product foreign key (idPOorder) references orders(idOrder)
);

create table storageLocation(
	idLproduct int,
    idLstorage int,
    location varchar(255) not null,
    primary key(idLproduct, idLstorage),
    constraint fk_storage_location_product foreign key(idLproduct) references product(idProduct),
    constraint fk_storage_location_storage foreign key (idLstorage) references productStorage(idProdStorage)
);
create table productSupplier(
	idPsupllier int,
    idPsProduct int,
    quantity int not null,
    primary key(idPsupllier,idPsProduct),
    constraint fk_product_supplier_supplier foreign key(idPsupllier) references supplier(idSupplier),
    constraint fk_product_supplier_product foreign key(idPsProduct) references product(idProduct)
    );

