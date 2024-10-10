# Projeto gRPC de Mensagens

Este projeto implementa um serviço gRPC simples que permite enviar mensagens entre um cliente e um servidor.

## Estrutura do Projeto

O projeto é composto por três partes principais:

1. **Protocolo de Mensagens**: Definição do serviço e das mensagens.
2. **Servidor**: Implementação do serviço que recebe mensagens.
3. **Cliente**: Envia mensagens para o servidor e recebe a resposta.

## Protocolo (messaging.proto)

```protobuf
syntax = "proto3";

package messaging;

// Definição do serviço
service MessagingService {
  rpc SendMessage (MessageRequest) returns (MessageResponse);
}

// Definição das mensagens
message MessageRequest {
  string content = 1;
}

message MessageResponse {
  string status = 1;
}
```
## Implementação do Servidor

```python
import grpc
from concurrent import futures
import time
import messaging_pb2_grpc
import messaging_pb2

class MyService(messaging_pb2_grpc.MyServiceServicer):
    def SendMessage(self, request, context):
        return messaging_pb2.MessageResponse(response=f"Mensagem recebida: {request.content}")

def serve():
    server = grpc.server(futures.ThreadPoolExecutor(max_workers=10))
    messaging_pb2_grpc.add_MyServiceServicer_to_server(MyService(), server)
    server.add_insecure_port('[::]:50051')
    server.start()
    print("Servidor rodando na porta 50051...")
    try:
        while True:
            time.sleep(86400)  # Aguarda indefinidamente
    except KeyboardInterrupt:
        server.stop(0)

if __name__ == '__main__':
    serve()
    

## Executando o Projeto

### Configuração

1. Instale as dependências necessárias:

    ```bash
    pip install grpcio grpcio-tools
    ```

2. Compile o arquivo `.proto` para gerar os arquivos Python necessários:

    ```bash
    python -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. messaging.proto
    ```
```

## Implementação do Cliente

```python
import grpc
import messaging_pb2_grpc
import messaging_pb2

def run():
    channel = grpc.insecure_channel('localhost:50051')
    stub = messaging_pb2_grpc.MyServiceStub(channel)

    try:
        response = stub.SendMessage(messaging_pb2.MessageRequest(content="Olá, gRPC!"))
        print("Cliente recebeu: " + response.response)
    except grpc.RpcError as e:
        print(f"Erro gRPC: {e.code()}, {e.details()}")

if __name__ == '__main__':
    run()
```
### Executar o Servidor

No terminal, execute o servidor:

```bash
python server.py
```

### Executar o Cliente

No terminal, execute o cliente:

```bash
python client.py
```
### Testando no Postman
![Reinicie o ciclo](https://github.com/LABELLECANDIDO/ExercicioLimonada/blob/main/app/src/main/res/imagens/copovazio.png)

### Recebendo no terminal
![Reinicie o ciclo](https://github.com/LABELLECANDIDO/ExercicioLimonada/blob/main/app/src/main/res/imagens/copovazio.png)


### Executar o Servidor

No terminal, execute o servidor:

```bash
python server.py
```

### Executar o Cliente

No terminal, execute o cliente:

```bash
python client.py
```
### Testando no Postman
![Reinicie o ciclo](https://github.com/LABELLECANDIDO/ExercicioLimonada/blob/main/app/src/main/res/imagens/copovazio.png)

### Recebendo no terminal
![Reinicie o ciclo](https://github.com/LABELLECANDIDO/ExercicioLimonada/blob/main/app/src/main/res/imagens/copovazio.png)
