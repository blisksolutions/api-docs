# Documentação de uso da API Blisk Solutions

## Autorização

A autorização é feita utilizando-se 2 cabeçalhos:

```
x-blisk-auth-key          AUTH_KEY_CLIENTE_AQUI
x-blisk-auth-value        AUTH_VALUE_CLIENTE_AQUI
```

Você poderá obter estas informações no Dashboard da Blisk acessando o menu Configurações ou solicitando diretamente com o seu administrador junto à Blisk.


## Requisição

### Leads

__POST__ https://api.blisk.solutions/leads

_Corpo em JSON_:

```json
{
    "midia": "1",
    "canal" : "1",
    "lead_id": "ID-LEAD-QUE-SE-DESEJA-ASSOCIAR",
    "lead_nome": "João Silva",
    "lead_email": "jsilva123@gmail.com",
    "lead_telefone": "11999999999",
    "lead_telefone2": "11988888888",
    "lead_telefone3": "11977777777",
    "produto_codigo": "CODIGO-DO-PRODUTO-QUE-SE-DESEJA-ASSOCIAR",
    "corretor_nome": "fulano da silva",
    "corretor_email": "fulanodasilva@suaempresa.com.br",
    "corretor_telefone": "11 9999-9999",
    "mensagem": "Gostaria de mais informações sobre o empreendimento xxxxxxxx"
}
```

__IMPORTANTE:__ Os campos obrigatórios são:

```
midia
lead_nome
lead_email
produto_codigo
```

SE algum dado do corretor for informado, todos os demais serão obrigatórios:

``` 
corretor_nome
corretor_email
corretor_telefone
```

Estes são os dados obrigatórios da Blisk, se os demais campos forem obrigatórios para sua empresa, a validação deverá ser feita do seu lado.


## Retorno

O retorno vai variar de acordo com os casos onde há erros ou sucesso.

__Em caso de erro__:

Verifique lista à frente detalhando os códigos de erro.

```json
{
    "status": "4xx",
    "errors" : [
        {
            "code" : "CODIGO",
            "message" : "MENSAGEM ERRO"
        }
    ],
    "totalErrors": "TOTAL"
}
```


__Em caso de sucesso__: 

"status" e "totalErrors" são oferecidos como facilidades

```json
{
    "status": 201,
    "totalErrors": 0,
    "success" : "Lead criado com sucesso!"
}
```

e

```json
{
    "status": 200,
    "totalErrors": 0,
    "success" : "Lead atualizado com sucesso!"
}
```


## Lista dos Códigos de Erro

Todos os erros retornados possuem __código__ e __mensagem__ e estão aqui somente para referência. 

| Código | Recurso      | Mensagem                                           |
|--------|--------------|----------------------------------------------------|
| A01    | Autenticação | Cabeçalho [x-blisk-auth-key] não informado         |
| A02    | Autenticaçao | Cabeçalho [x-blisk-auth-value] não informado       |
| A03    | Autenticaçao | Cliente não autorizado. Verifique suas credenciais |
| L00    | Lead         | Não foi possível salvar o Lead                     |
| L01    | Lead         | Nome do Lead não informado                         |
| L02    | Lead         | Email do Lead não informado                        |
| P00    | Produto      | Não foi possível salvar o Produto                  |
| P01    | Produto      | Código do Produto não informado                    |
| M00    | Comunicação  | Não foi possível salvar o Contato                  |
| M01    | Comunicação  | Mídia não informada                                |
| C00    | Corretor     | Não foi possível salvar o Corretor                 |
| C01    | Corretor     | Nome do Corretor não informado                     |
| C02    | Corretor     | Email do Corretor não informado                    |
| C03    | Corretor     | Telefone do Corretor não informado                 |


Fim.
