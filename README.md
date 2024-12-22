# O que é esse projeto?

# O que é necessário?
- conta aws
- conta no  https://www.tomorrow.io/

# Desenho da arquitetura?
veja na pasta resources

## steps
### 1 - criar o kinesis com o nome [broker]
### 2 - criar a role para o produtora com o nome [producer_iam]
    -   coloque o usecase lambda, pois é ele que vai usar
    -   coloque as permissoes: 
        - AWSLambdaBasicExecutionRole
        - AmazonKinesisFullAccess
### 3 - criar a lambda producer
    - a funcao lambda ja esta zipada e esta no pacote de resources.
    - a versao do pyton recomentada é a Python 3.12
    - associe a role [producer_iam]
    - será necessario colocar colocar as constantes (as variaveis de ambiente)
        - vá em environment variables e adicione.:
            TOMORROW_API_KEY: xptoAPIKEYDOTOMORROW.IO 
### 4 - criar topico sns
    - crie o topico com o nome [snsalerta]
    - crei a subscription Email
    - crei a subscription SMS
### 5 - criar a role para o consumidora com o nome [consumerrealtime_iam]
    -   coloque o usecase lambda, pois é ele que vai usar
    -   coloque as permissoes: 
        - AmazonSNSFullAccess
        - AmazonLambdaKinesisExecutionRole
### 6 - criando consumer real time
    - altere o nome do SNS_TOPIC_ARN
    - a funcao lambda esta na pasta resource. Copie e cole
    - será necessario colocar colocar as constantes (as variaveis de ambiente)
        - vá em environment variables e adicione.:    
            PRECIPITATION_PROBABILITY: 70
            WIND_SPEED: 10
            WIND_GUST: 15 -> coloque zero pra forcar uma atualizacao
            RAIN_INTENSITY: 5
    - importante.:: agora adicione um trigger a essa lambda function
        source.: kinesis
        coloque.: broker
### 7 - criando cloudwatch crie com o nome de [producer_event]
    - Amazon EventBridge>Rules>Create rule
    - coloque o type schedule
    - coloque o rate-based schedule
    - coloque o invoke Lambda function [producer]
    - lembre de desativar pra nao ficar pingando na api desnecessariamente
    
    

