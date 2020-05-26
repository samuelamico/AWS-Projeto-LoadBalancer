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


