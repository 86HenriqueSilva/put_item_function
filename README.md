# put_item_function
Amazon Cognito

Importações:

import json
import boto3

As importações acima são necessárias para usar as bibliotecas json e boto3 em nosso código.
A biblioteca json é usada para analisar o JSON enviado na requisição, e a biblioteca boto3 é usada para interagir com o Amazon DynamoDB da AWS.

    Configuração do DynamoDB:
    
   dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Items')

O código acima cria um recurso do DynamoDB usando o boto3.resource e especifica o nome da tabela que será utilizada.

    Função Lambda:
    
    def lambda_handler(event, context):
    response_body = ""
    status_code = 0

    data = json.loads(event['body'])
    id = data['id']
    price = data['price']
    
    Esta é a função principal que será executada quando a função Lambda for acionada. 
    O evento é recebido como argumento da função, e o corpo da requisição é extraído usando o event['body'].
    Em seguida, o corpo é analisado com o json.loads para obter o valor do id e do price.

    Operação Put no DynamoDB:
        try:
        table.put_item(
            Item={
                'id': id,
                'price': price
            }
        )
        status_code = 200
        response_body = json.dumps('Item inserido com sucesso!')
        except Exception as e:
        status_code = 200
        response_body = json.dumps(str(e))
        
        O código acima faz a operação put_item no DynamoDB.
        O Item que será inserido é definido com o id e o price. 
        Se a operação for concluída com sucesso, o código define o status_code como 200 e define a response_body como uma mensagem indicando que o item foi         inserido com sucesso. 
        Se a operação falhar, o status_code será definido como 200 e a response_body será definida como a mensagem de erro.

    Retorno da Função Lambda:
        response = {
        'statusCode': status_code,
        'body': response_body
    }
    
    return response
    
    O código acima define o objeto de resposta que será retornado pela função. Ele contém o statusCode e a response_body definidos anteriormente. A função retorna esse objeto de resposta.





