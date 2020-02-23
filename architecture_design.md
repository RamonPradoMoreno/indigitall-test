# Architecture Design

For the architecture design I will go through some general design decision then draw a basic diagram and, at last, explain all the different parts.

## General design

Since this is a small team and there is no systems engineer I would recommend to use a cloud service provider. They usually have simple web interfaces and [serverless applications](https://aws.amazon.com/es/serverless/) that require 0 maintenance. I would use [AWS](https://aws.amazon.com/es/what-is-aws/?nc2=h_ql_le_int) because I have experience using it and find it extremely complete and easy to use.

All decisions should be discussed with all the team but since I cannot do that I'm assuming that AWS will be used and all my recommendations followed. I have not tested all of this and don't have practical experience with all the modules but based on the docs I have read I think it will work and would love to do it. :)

## Diagram

## Module Explanation

### CloudWatch Service

[Cloudwatch](https://aws.amazon.com/cloudwatch/?nc1=h_ls) is the AWS logging and monitoring tool. It is integrated with almost all other AWS tools making this process much easier than in a company developed environment. It will take care of:

* Gathering all our system logs and monitor all the pieces.
* Optimize resource utilization.
* Automatically register relevant metrics and detect anomalous behavior.

The yellow arrows in the diagram indicate that the data exchange is not of business information but logging and monitoring data.

### Database

For the database I would use [Amazon Aurora](https://aws.amazon.com/es/rds/aurora/serverless/) because it is:

* Compatible with PostgreSQL &rarr; We don't need a noSQL database, it is open source, used extensively.
* Serverless &rarr; Does not require instance managing and The database will automatically start up, shut down based on your application needs.
* Automatic scalability &rarr; The database resources will be automatically managed to match application needs.
* Pay for use only &rarr; The company will only be charged for what is used. Since we are not having a lot of clients this will be very cost effective.

### API Gateway

The [api gateway](https://aws.amazon.com/api-gateway/) is the only entrance to our backend. It makes sure that some security standards are met: takes care of authentication and authorization, logging and endpoint monitoring among other things.

I think this is a key piece of the architecture because, from a simple UI you can control the access to all your endpoints using, for example API keys for third party developers. It also has integration with Cloudwatch.

### Microservices

Microservices are simple applications that take care of one "relatively simple" job. Instead of working on an application that solves all our problems we will break our problems in simpler problems and create a microservice for each one of them. This is done to avoid complex applications and isolate functionalities. If there is a problem it will not affect all the system, only one of our microservices.

To make the deployment of our microservices easy I suggest to use [Docker](https://www.docker.com/why-docker) because:

* It makes sure that the environment where our application is tested and used never changes (avoiding the classic "It was working a minute ago! what happened?!"). 
* Docker allows for horizontal scalability, this means that if a microservice is too busy you can quickly start a new one and move some of the load to it.
* A lot of microservice frameworks have docker integrations such as [Quarkus](https://quarkus.io/) for Java microservices. Python's Flask does not have it but deployment on a container is not hard at all.
* You can automate the container build process and sync it with code repositories so when a code is pushed it is automatically uploaded and a container started with the new code in the development/testing environment. (This is done using [docker hub](https://hub.docker.com/))

AWS, as always, knows about this stuff and has serverless integration with Docker's containers through the [Amazon Elastic Container Service](https://aws.amazon.com/ecs/) and [AWS Fargate](https://aws.amazon.com/fargate/). This means that container management will not require server maintenance  and will be done easily. (The docs say it is easy but I've checked and it does not look that easy without a systems engineer, there are other alternative and maybe easier ways of doing it.)



Diseña una arquitectura para almacenar, limpiar, explotar y presentar estos datos. El uso de esta plataforma será:

* Dispondrá de información de niveles de NO2, las estaciones donde se han recogido y datos de temperaturas de Madrid
* Hay dos tipos de cargas de información:

    * Masivas, puntuales: sirven para hacer una carga inicial de datos. También, de forma esporádica, para corregir información capturada en tiempo real.
    * Incrementales. Los orígenes son:

        * Datos en tiempo real (actualizados cada hora) de contaminación, más información [aquí](https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=41e01e007c9db410VgnVCM2000000c205a0aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default)
        * Datos de temperaturas. Se capturarán consultando alguna API de servicios metereológicos.

* La explotación será:

    * Vía API: los usuarios de la plataforma pueden consultar y descargar los datos por API.
    * Vía portal web: el equipo de Front diseñará un portal para permitir que los usuarios visualicen mapas de calor, gráficas de evolución, etc.
    * Modelo predictivo: el equipo de Data creará un modelo para predecir la contaminación de los próximos 3 días.
    * Análisis _adhoc_: además, el equipo de Data necesita explorar y crear pequeños análisis _adhoc_ que puedan surgir. P.e. prevemos que el Ayuntamiento nos asigne la tarea de medir el efecto de las medidas tomadas en la legislatura pasada: Madrid Central, restricciones los días de aviso de contaminación, etc.

* El volumen de los datos: profundidad histórica desde el año 2001.
* La cantidad de usuarios: 500-1000 usuarios diarios.
* Las características de nuestro equipo: somos una _startup_ pequeña y tecnológica, con unos pocos perfiles por disciplina: _front_, _back_ y _data_. No tenemos perfiles especializados de sistemas.

No hace falta que programes nada en esta parte. Simplemente describe en la forma que creas más conveniente cómo lo harías (p.e. con un diagrama de arquitectura + comentarios).

### Anexo

Puedes ver la información adicional aquí:

* [Estaciones de medida](https://gist.github.com/koldLight/533038c852ca0a546da247292b5d9ab9)
* [Temperaturas horarias](https://gist.github.com/koldLight/90577c60ad4267d4df490e6239cebf58)