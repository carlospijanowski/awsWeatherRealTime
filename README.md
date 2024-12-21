# O que é esse projeto?

# O que é necessário?
1 - conta aws
2 - conta no  https://www.tomorrow.io/

# Desenho da arquitetura?
veja na pasta resources

# steps
1 - criar o kinesis com o nome [broker]
2 - criar a role para o producer_iam com o nome [producer_iam]
    -   coloque o usecase lambda, pois é ele que vai usar
    -   coloque as permissoes: 
        - AWSLambdaBasicExecutionRole
        - AmazonKinesisFullAccess
