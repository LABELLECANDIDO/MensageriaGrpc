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
