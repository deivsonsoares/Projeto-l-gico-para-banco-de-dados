#inserção de dados queries
use ecommerce;
show tables;
# idClient, Fname, Minit, Lname, CPF, Address
insert into Clients( Fname, Minit, Lname, CPF, Address)
	values('Maria','M','Silva',12346789,'rua silva de prata 29, carangola - Cidade das Flores'),
			('Ana','S','resenha',987654321,'rua almeida 231, Flores - Caxias'),
            ('Doralice','F','Santos',45678913,'rua rosaura 250, monte - Bento'),
            ('Joao','P','antonio',789123456,'rua epifanio 1243, mariante - Farroupilha'),
            ('Dorvalino','S','ermelindo',98745631,'rua equina dobrada 1098, nilo - Porto alegre'),
            ('Jarelino','R','juventu',654789123,'rua umdoitrequatro, meia duzia - mato grosso');
# idProduct, Pname, Classification_kids Boolean, category('Eletrônico','Vestimenta','Brinquedos','Alimentos','Móveis'), avaliação, size
insert into product (Pname, Classification_kids, category, avaliation, size) values
	('Fone de ouvido', false,'Eletrônico','4',null),
    ('Barbie Elsa', true,'Brinquedo','3',null),
    ('Body Carters', true,'Vestimenta','5',null),
    ('Microfone Vedo - Youtuber', false,'Eletrônico','4',null),
    ('Sofá retrátil', False,'Móveis','3','3x57x80');
    
select * from clients;
select * from product;
#idOrder, idOrderClient, orderStatus, Description, sendValue, paymentCash
insert into orders(idOrderClient, orderStatus, Description, sendValue, paymentCash)values
		(1,default,'compra via aplicativo', null,1),
        (2,default,'compra via aplicativo', 50,0),
        (3,'Confirmado',null, null,1),
        (4,default,'compra via web site', 150,0),
        (2,default,'compra via aplicativo', null,1);
#idPOproduct, idPOorder, poQuantity, poStatus
select * from orders;
insert into productOrder(idPOproduct, idPOorder, poQuantity, poStatus) values
			(1,5,2,null),
            (2,5,1,null),
            (3,6,1,null);
#storageLocation, quantity
insert into productStorage (storageLocation, quantity) values
					('Rio de Janeiro', 1000),
                    ('Rio de Janeiro', 500),
                    ('São Paulo', 10),
                    ('São Paulo', 100),
                    ('São Paulo', 10),
                    ('Brasilia', 60);
                    
#idLproduct, idLstorage, location
insert into storageLocation(idLproduct, idLstorage, location)   values
					(1,2,'RJ'),
                    (2,6,'GO');
#idSupplier, SocialName, CNPJ, Contact
insert into supplier(SocialName, CNPJ, Contact) values
	('Almeida e filho','123456789123456','21985474'),
    ('Eletrônicos Silva','854519649143457','21985484'),
    ('Elet´ônicos Valma','934567893934695','21975474');
    
    select * from supplier;
#idPsSupplier, IsPsProduct, quantity
insert into productSupplier(idPsSupplier, IdPsProduct, quantity) values
		(1,1,500),
        (1,2,400),
        (2,4,633),
        (3,3,5),
        (2,5,10);
            
#idSeller, SocialName, AbstName, CNPJ,CPF,location,contact
insert into seller(SocialName, AbstName, CNPJ,CPF,location,contact)   values
				('Tech eletonics',null, '123456789456321',null,'Rio de Janeiro',219946287),
				('Boutique Durgas',null, '123456783',null,'Rio de Janeiro',219567895),
                ('Kids world',null, '456789123654485',null,'São Paulo',1198657484);
select * from seller;
#idPseller, idePproduct, prodQuantity
 insert into productSeller(idPseller, idePproduct, prodQuantity) values              
               (1,6,80),
               (2,7,10);
               
select * from productSeller; 
#recuperando numero de clientes existentes
select count(*) from clients;
#verificando os pedidos feitos pelos cliente              
select *from clientes c, orders o where c.idClient = idOrderClient;               
#especificando os atributos que estao sendo recuperados
select Fname,Lname, idOrder, orderStatus from clientes c, orders o where c.idClient = idOrderClient;
#especificando os atributos que estao sendo recuperados, melhorando a visualizacao 
select (Fname,'',Lname)as client, idOrder as Request, orderStatus as status from clientes c, orders o where c.idClient = idOrderClient;
    
#agrupando consulta
select count(*)from clients c, orders 
			where c.idClient = idOrderClient;
#consulta tb cliente que nao fizeram pedidos
select * from clients left outer join orders ON idClient = idOrderClient
inner join product; 
  
  #clientes que fizeram pedidos
  select * from clients c inner join orders o ON c.idClient = o.idOrderClient
			inner join productOrder p on p.idPOorder = o.idOrder; 

#clientes que fizeram pedidos agrupando  
#quantos pedidos foram realizado pelos clientes?
  select c.idClient, Fname,count(*) as Number_of_orders from clients c inner join orders o ON c.idClient = o.idOrderClient
			inner join productOrder p on p.idPOorder = o.idOrder
            group by idclient; 
            