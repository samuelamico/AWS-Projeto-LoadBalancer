# AWS-Projeto-LoadBalancer

-------------------------------------------------------------------------------------------------------------------------

O objetivo é criar uma aplicação que envolva vários serviçoes da AWS e que seja uma aplicação distribuida e balanceada. O projeto pode ser descrito nas imagens abaixo:


![Aplicação](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Aplicacao_projeto.png)

A aplicação vai utilizar O storage S3, O banco de dados RDS e duas instâcias EC2 e um Load Balancer. Porém, para que a aplicação esteja balanceada, quando for necessário as instancias EC2 irão escalonar, como mostra a imagem abaixo:


![Aplicação Balanceada](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Aplicacao_projeto2.PNG)


------------------------------------------------------------------------------------------------------------------------

## Parte 1. Criar Instância EC2

O primeiro passo antes de criar a instância EC2 é configurar um função IAM, que tem como objetivo
fazer com que as nossas instâncias acessem o storage S3 com permissão apenas de Leitura.

![IAM](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Funcao_IAM.PNG)

Após criar a função é necessário criar a Instancia. A imagem da nossa instância foi a Amazon Linux

![Image Instance](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Ec2-Image.PNG)

Foi colocado um Code deploy, para instalar e configurar toda a aplicação necessária:


![Code Deploy](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Install.PNG)

A seguinte configuração de segurança foi utilizada, iremos usar a porta 80 para nossa aplicação web:

![Security Group](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Security_group.PNG)

Por fim, criamos nossa Instância:

![Instância](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Instancias.PNG)

E podemos acessar o endereço IPV4 publico para checarmos nossa aplicação:

![Aplicação](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Instancia_show.PNG)


------------------------------------------------------------------------------------------------------------------------

## Parte 2. Criar RDS, S3 e replicar instância EC2

### Banco RDS

O Banco rds é o nosso sistema SaaS , onde utilizaremos um banco SQL para nossa aplicação.

![RDS-SQL](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/RDS1.PNG)

![RDS-SQL](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/RDS2.PNG)

![RDS-SQL](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/RDS3.PNG)


![RDS-SQL](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/RDS4.PNG)

Após a criação do RDS, precisamos criar uma política VPC para que apenas nossas instancias EC2 acessem o banco
SQL.

![RDS-VPC](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/VPC-RDS.PNG)


Editamos nossa RULES:

![VPC-RDS-Rules](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/VPC-RDS-2.PNG)


### S3

Vamos criar um bucket S3 para armazenar imagens para serem utilizadas na nossa aplicação:

![S3](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/S3.PNG)

![S3-Permissao](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/S3-2.PNG)

Configurar a Policy:

![S3-Policy](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/S3-Policy.PNG)

![S3-Policy](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/Politica-S3.PNG)

![S3-Policy](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/Politica_IAM_s3.png)

Configurar a hospedagem da imagem:

![S3-Site](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/S3-Site.PNG)


### Usario

O Usuario novo tem permissao para colocara imagens na aplicação, ou seja no S3. Para criar um usuario é preciso
entrar no VPC - CreateUser

![User-VPC](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/VPC-User.PNG)

![User-VPC](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/Usuario_s3.png)


É preciso criar uma politica nova para o usario:

![User-Per](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/User-Permission.PNG)

![User-Policy](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/User-Policy.PNG)


### Replicate EC2

Para replicar a instancia EC2 foi necessário criar uma imagem da instancia ja criada e criar uma nova apartir da imagem.

![Replicate-EC2](https://github.com/samuelamico/AWS-Projeto-LoadBalancer/blob/master/Img/Parte2/New-Instance.PNG)