<img src="https://content.pstmn.io/ac0c27a3-91a6-493e-90cc-de99bfd14ac3/bG9nb21hY2hpbmVidy5wbmc=">

Bem-vindo à API da Machine! Este documento guiará você na integração do seu sistema com o nosso de maneira simples e eficaz.

Para garantir uma integração tranquila e bem-sucedida, é essencial ter todas as informações necessárias à mão. A Machine está em constante evolução, por isso, recomendamos acompanhar nossos informes e o changelog para se manter atualizado sobre as novidades na integração.

## Quem Somos?

A Machine é um produto [Gaudium](https://www.gaudium.global/), projetado para fornecer tecnologia que permite a operação eficiente e segura das centrais (empresas de mobilidade urbana, como transporte de passageiros e entregas). Nossa plataforma oferece a tecnologia necessária para que os condutores possam realizar seus serviços, movimentando-se do ponto A ao ponto B conforme as solicitações recebidas.

## Tipos de Solicitações e Formas de Pagamento

As solicitações podem ser feitas de imediato ou programadas para o futuro, cada uma identificada por números diferentes. Após o disparo de uma solicitação programada, uma nova solicitação é criada no sistema. Todas as solicitações estão associadas a uma forma de pagamento. As opções de pagamento incluem:

- Dinheiro (`D`).
    
- Débito (`B`).
    
- Crédito (`C`).
    
- Pix (`X`).
    
- PicPay (`P`).
    
- WhatsApp (`H`).
    
- Faturado (`F`).
    
- Carteira de Créditos (`R`).
    

As solicitações de entregas podem ter vários objetivos, dependendo do modelo de negócio e do tipo de cliente:

- **Entrega de refeições**: Levar a refeição de um restaurante até o cliente final.
    
- **Entrega de encomendas**: Levar encomendas de lojas ou centrais de distribuição até o cliente final.
    

## Agentes das Solicitações e Estimativas

Os principais agentes das solicitações são os condutores (entregadores). Para otimizar seu negócio, é possível criar categorias e associar os condutores a elas, como uma categoria específica para carregar produtos delicados. Antes da solicitação, a empresa pode obter uma estimativa de custo, que é sempre feita por categoria. Cada categoria tem suas tarifas definidas pela central.

## Ciclo de Vida das Solicitações

As solicitações de entregas passam por várias etapas e subetapas, detalhadas a seguir. Nota-se que os registros de solicitação não alteram o status da solicitação

- **Distribuindo (**`D`**)**: Solicitação aberta e ainda não atribuída a um condutor.
    
- **Aguardando aceite (**`G`**)**: Esperando um condutor aceitar a solicitação.
    
- **Pendente ou Buscando Condutor (**`P`**)**: Solicitação não aceita, aguardando aceitação.
    
- **Não atendida (**`N`**)**: Nenhum condutor aceitou a solicitação.
    
- **Aceita (**`A`**)**: Solicitação aceita por um condutor.
    
    - **A Caminho**: Condutor está a caminho do local de coleta do pedido.
        
    - **Aguardando no Estabelecimento**: Condutor chegou ao local de coleta.
        
- **Em andamento (**`E`**)**: Condutor coletou o pedido e iniciou a entrega.
    
- **Finalizada (**`F`**)**: Condutor entregou o pedido no local de destino.
    
- **Em Espera (**`S`**)**: Solicitação em espera até a conclusão de uma anterior.
    
- **Cancelada (**`C`**)**: Solicitação cancelada
    

## Solicitações Programadas

Solicitações aceitas e canceladas por um condutor antes do início podem ser redistribuídas, ocasionando a repetição de alguns status. Solicitações programadas seguem um ciclo específico de estados:

- **Aguardando (**`A`**):** Aguardando horário de disparo.
    
- **Disparada (**`D`**):** Solicitação programada disparada.
    
- **Cancelada (**`C`**):** Solicitação cancelada.
    
- **Erro (**`X`**):** Problema no processo da solicitação.
    

## Primeiros Passos

Passos iniciais para iniciar sua integração com a Machine:

1. **Autorização**: Utilize uma API key e um login válido. Caso você seja um usuário de central, entre em contato com o nosso suporte. Caso contrário, entre em contato com a central responsável pela integração para mais informações.
    
2. **Importe essa documentação para o Postman**: Acesse o link da coleção no Postman fornecido e importe o arquivo JSON da coleção diretamente no Postman.
    
3. **Atualize as variáveis**: Configure as variáveis de ambiente no Postman (descritas na seção "Variáveis da coleção"), conforme necessário.
    

Pronto! Agora você está preparado para explorar a nossa integração para que, juntos, possamos crescer ainda mais.

## [Rate Limit](#ratelimit)

Por padrão, a maioria dos endpoints tem um limite de 50 requisições por minuto. No entanto, alguns endpoints podem ter limites diferentes, conforme listado abaixo:

| **Endpoint** | **Rate Limit** |
| --- | --- |
| /api/integracao/solicitacaoStatus  <br>/api/integracao/sacarCreditosCondutor  <br>/api/integracao/saldoCreditosCondutor  <br>/api/integracao/recarregarCreditosCondutor  <br>/api/integracao/enviarMensagem  <br>/api/integracao/atualizarEmpresa  <br>/api/integracao/sacarCreditosEmpresa  <br>/api/integracao/saldoCreditosEmpresa  <br>/api/integracao/recarregarCreditosEmpresa | 4 requests/minuto. |
| /api/integracao/solicitacao  <br>/api/integracao/recibo  <br>/api/integracao/posicaoCondutor  <br>/api/integracao/abrirSolicitacao | 100 requests/minuto. |
| /api/integracao/consultarProgramada  <br>/api/integracao/condutor | 200 requests/minuto. |

## Autorização.

- A Machine utiliza uma chave de API para autorização.
    
- Você deve incluir uma chave de API em cada requisição à API da Machine com o cabeçalho `api-key`.
    
- A chave de API foi pré-preenchida como uma variável da coleção.
    
- Para se autenticar ao nosso sistema você deve realizar uma autenticação básica, isto é, deve informar o login e a senha de um usuário ativo da sua central ou empresa.
    

A autorização e login foi configurado no nível da coleção, então todas as requisições nesta coleção herdarão automaticamente o cabeçalho necessário para a autenticação básica.

⚠ **Lembre-se de que a sua api-key, quando usada em conjunto com a autenticação básica, concede acesso a todos os recursos e é o que define qual central está acionando a nossa API. Portanto, é crucial que os responsáveis mantenham-nas em locais seguros e não as exponham no lado do cliente da aplicação**. [<b>Saiba mais sobre o uso de variáveis no Postman</b>](https://learning.postman.com/docs/sending-requests/variables/#initial-and-current-values)

## Usuário Autenticado

O usuário autenticado é a entidade utilizada para realizar as requisições na API da Machine. Assim como qualquer outro, este possui um cargo e suas permissões. O usuário autenticado terá acesso às endpoints conforme às permissões concedidas na seção Integração em: **Minha equipe > Usuário > Permissões**.

Há dois logins que permitem acesso às endpoints: login de empresa (quando o usuário é de uma empresa) e o login da central (quando o usuário é da central). O login também irá limitar alguns acessos, pois usuários de empresa terão acesso apenas às informações associadas a sua empresa.

## Padrão da API

A nossa API segue o padrão REST e todas as suas respostas são em JSON.

Usamos como retorno os códigos HTTP padrão para indicar tanto o sucesso de uma requisição, quanto para indicar falhas. Os principais retornos são:

- **200**: Sucesso.
    
- **400**: Os dados serão validados e, se faltar algum parâmetro obrigatório, será gerado um código de retorno HTTP 400. Outros erros de validação, como erros associados a regra de negócio, serão tratados com códigos de erro específicos e mensagens explicativas.
    
- **404**: Endpoint não encontrado, revise a URL passada.
    
- **500**: Erro interno, contate o nosso suporte.
    

Caso ocorra algum erro na autenticação básica, um erro padrão de código 1 informando “usuário e/ou senhas inválidas”, será retornado.

Caso a chave API não seja informada, um erro padrão será retornado:

``` json
{
    "success": false,
    "errors": [
      "Chave da app não informada."
    ]
}

 ```

## Variáveis da coleção

A coleção utiliza das seguintes variáveis:

| Variáveis | Descrição |
| --- | --- |
| `base_url` | Deve conter a URL em que será feita as requisições. |
| `default_api_key` | Deve conter a sua chave API. |
| `basic_auth_username` | Deve conter o login do usuário autenticado. |
| `basic_auth_password` | Deve conter a senha do usuário autenticado. |

## Changelog

Para ficar por dentro de todas as atualizações e melhorias que implementamos, recomendamos que você verifique nosso [changelog](https://www.machine-updates.com/) regularmente. Nele, você encontrará um registro detalhado de todas as mudanças, correções de bugs e novos recursos adicionados ao nosso sistema.


Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Central
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
Cupom
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
GET
Obter geradores
https://api-trial.taximachine.com.br/api/integracao/geradorCupom
Essa endpoint retorna todos os geradores de cupons criados pela central. Atualmente, essa é uma funcionalidade em beta, para criar o seu gerador de cupom, por favor, contate o nosso suporte. É necessário informar apenas o api-key.

Para ter acesso a essa endpoint, é necessário que o usuário tenha a permissão "API - Cupom"
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622


GET /api/integracao/geradorCupom HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7



{
    "success": true,
    "response": [
        {
            "id": "493",
            "nome": "ut",
            "tipo": "ate_n_vezes_por_passageiro",
            "data_hora_inicio": "2001-01-01T00:00:00Z",
            "data_hora_fim": "2001-01-01T23:59:59Z",
            "limite_uso_individual": "237",
            "quantidade_maxima_cupons": "995",
            "quantidade_cupons_gerados": "0",
            "tipo_desconto": "percentual",
            "desconto": "495.09",
            "tipos_pagamentos": [
                {
                    "tipo": "D",
                    "nome": "Dinheiro"
                },
                {
                    "tipo": "B",
                    "nome": "Débito (máquina)"
                },
                {
                    "tipo": "C",
                    "nome": "Crédito (máquina)"
                },
                {
                    "tipo": "F",
                    "nome": "Faturado"
                },
                {
                    "tipo": "X",
                    "nome": "Pix"
                },
                {
                    "tipo": "P",
                    "nome": "Picpay"
                },
                {
                    "tipo": "H",
                    "nome": "Whatsapp"
                },
                {
                    "tipo": "R",
                    "nome": "Carteira de Créditos"
                }
            ]
        }
    ]
}




POST
Criar cupom
https://api-trial.taximachine.com.br/api/integracao/criarCupom
Essa endpoint permite a criação de um cupom, conforme as regras estabelecidas no gerador de cupom. É obrigatório existir um gerador de cupom, para que seja possível criar cupons pela nossa API.

Para ter acesso a essa endpoint, é necessário que o usuário tenha a permissão "API - Cupom"
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Body
raw (json)


{
    "gerador_cupom_id": 1,
    "codigo": "teste",
    // "codigo_pattern": "{as134da4sf}",
    "data_hora_inicio": "2024-02-10T03:46:15Z",
    "data_hora_final": "2024-02-15T03:46:15Z",
    "limite_de_uso": "ate_n_vezes_por_passageiro",
    "limite_de_uso_individual": 1,
    "tipo_desconto": "percentual",
    "desconto": 32.01,
    "observacao": "5.00",
    "tipos_pagamentos": [
        "D"
    ]
}

GET
Obter categorias
https://api-trial.taximachine.com.br/api/integracao/categoria
Retorna às categorias ativas da central. Caso seja informada uma localização pertencente a uma filial, serão retornadas as categorias ativas da filial. Caso seja informada a latitude e longitude, não é necessário passar as demais informações.

﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Query Params
endereco
<string>
Endereço do solicitante interessado em saber as categorias. Obrigatório apenas na ausência dos parâmetros lat e lng.

bairro
<string>
Bairro do solicitante interessado em saber as categorias. Obrigatório apenas na ausência dos parâmetros lat e lng.

cidade
<string>
Cidade do solicitante interessado em saber as categorias. Obrigatório apenas na ausência dos parâmetros lat e lng.

estado
<string>
Estado do solicitante interessado em saber as categorias. Obrigatório apenas na ausência dos parâmetros lat e lng.

lat
<float><string>
Latitude da localização do solicitante interessado em saber as categorias. Obrigatório caso envie lng.

lng
<float><string>
Longitude da localização do solicitante interessado em saber as categorias. Obrigatório caso envie lat.

Example
200 - Por local de partida
Request
View More
HTTP
GET /api/integracao/categoria?endereco_partida=Rua Evandro Câmara, 717&bairro_partida=Monte Carmelo&cidade_partida=Montes Claros&estado_partida=MG HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (12)
View More
json
{
    "success": true,
    "response": [
        {
            "id": "57",
            "nome": "consequatur"
        },
        {
            "id": "678",
            "nome": "perferendis"
        },
        {
            "id": "565",
            "nome": "minima"
        },
        {
            "id": "635",
            "nome": "vitae"
        }
    ]
}
POST
Enviar Mensagem
https://api-trial.taximachine.com.br/api/integracao/enviarMensagem
Permite que a CENTRAL enviar mensagem para empresa ou condutor, tanto de forma privativa como de forma geral.

O tipo_chat pode ser descrito para qual conversa a central gostaria de enviar a mensagem. Cada tipo de chat, possui um propósito específico:

E: Chat empresa <-> central
C: Chat central <-> empresa
G: Chat central <-> condutores
P: Chat central <-> condutor
Além disso, o campo destinatario_id é apenas obrigatório, para os tipos de chat E e P. Para o chat do tipo E é o identificador da empresa, enquanto para o chat do tipo P é o identificador do condutor.

Para ter acesso a essa endpoint, é necessário que o usuário tenha a permissão "API - Mensagem"
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (json)
json
{
    "tipo_chat": "<char>",
    "destinatario_id": "<int>",
    "mensagem": "<string>"
}
Example
400 - Campo tipo_chat inválido (string)
Request
HTTP
POST /api/integracao/enviarMensagem HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 105

{
    "tipo_chat": "INVALIDO",
    "destinatario_id": 10,
    "mensagem": "Esta é uma mensagem exemplo"
}
400 Bad Request
Response
Body
Headers (9)
json
{
    "success": false,
    "errors": [
        {
            "code": 108,
            "message": "Campo tipo_chat é inválido. Valores possíveis: E,C,P,G."
        }
    ]
}
GET
Obter documentos
https://api-trial.taximachine.com.br/api/integracao/obterDocumentos
Esse endpoint é responsável por retornar todos os documentos criados pela central. Não são necessários parâmetros extras.

﻿

Example
200 - Obter documentos
Request
HTTP
GET /api/integracao/obterDocumentos HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (12)
View More
json
{
    "success": true,
    "response": {
        "documentos": [
            {
                "nome": "Alvará de táxi",
                "tipo": "ZG9jXzEy",
                "ativo": false
            },
            {
                "nome": "Certidão de antecedentes criminais",
                "tipo": "ZG9jXzEx",
                "ativo": false
            },
            {
                "nome": "CNH (Carteira Nacional de Habilitação)",
                "tipo": "ZG9jXzg",
                "ativo": true
            },
            {
                "nome": "Comprovante de residência",
                "tipo": "ZG9jXzk",
                "ativo": false
            },
            {
                "nome": "CRLV (Certificado de Registro e Licenciamento do Veículo)",
                "tipo": "ZG9jXzEw",
                "ativo": true
            },
            {
                "nome": "quos omnis dolor",
                "tipo": "ZG9jXzE2OQ",
                "ativo": true
            }
        ],
        "quantidade_documentos": 6
    }
}
GET
Obter áreas bloqueio
https://api-trial.taximachine.com.br/api/integracao/listarAreas
Endpoint responsável por listar as áreas de bloqueio disponíveis para central.

Funciona em formato de paginação, podendo passar os parâmetros limite e pagina para especificar o limite por página, e qual página deseja visualizar, respectivamente.

﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Query Params
limite
886
pagina
201
Example
200 - Sucesso
Request
HTTP
GET /api/integracao/listarAreas HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: •••••••
200 OK
Response
Body
Headers (10)
View More
json
[
    {
        "id": "1",
        "nome": "Abelardo Bueno"
    },
    {
        "id": "2",
        "nome": "01"
    },
    {
        "id": "3",
        "nome": "02"
    },
    {
        "id": "4",
        "nome": "03"
    },
    {
        "id": "5",
        "nome": "04"
    },
    {
        "id": "7",
        "nome": "06"
    },
    {
        "id": "8",
        "nome": "07"
    },
    {
        "id": "9",
        "nome": "08"
    },
    {
        "id": "10",
        "nome": "09"
    },
    {
        "id": "11",
        "nome": "10"
    },
    {
        "id": "12",
        "nome": "11"
    },
    {
        "id": "13",
        "nome": "12"
    },
    {
        "id": "14",
        "nome": "13"
    },
    {
        "id": "15",
        "nome": "14"
    },
    {
        "id": "16",
        "nome": "15"
    },
    {
        "id": "17",
        "nome": "16"
    },
    {
        "id": "18",
        "nome": "17"
    },
    {
        "id": "19",
        "nome": "18"
    },
    {
        "id": "20",
        "nome": "22"
    },
    {
        "id": "21",
        "nome": "25"
    }
]
Entregador
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
Documento
Atributo	Descrição
tipo_identificacao
I - Id, C - CPF, V - VTR, T - Telefone, P - Placa
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
POST
Atualizar documento
https://api-trial.taximachine.com.br/api/integracao/documentoCondutor/<int>
Esse endpoint permite a atualização de dados do condutor. São alterados apenas os atributos enviados, os demais atributos não são alterados.

﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
form-data
tipo
<string>
(Required). Tipo do documento a ser enviado. Deve verificar o valor na endpoint obterDocumentos (seção da central), ou enviar o tipo 'rosto' quando for foto do rosto.

foto
postman-cloud:///1ee9b714-13f4-47e0-8500-90c8b8418eeb
(Required). Upload da foto a ser inserida no documento

Example
200 - Atualizar documento entregador
Request
View More
HTTP
POST /api/integracao/documentoCondutor/{{entregador_id}} HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 303
Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW

------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="tipo"

{{tipo_documento_cnh}}
------WebKitFormBoundary7MA4YWxkTrZu0gW
Content-Disposition: form-data; name="foto"; filename="[PROXY]"
Content-Type: <Content-Type header here>

(data)
------WebKitFormBoundary7MA4YWxkTrZu0gW--
200 OK
Response
Body
Headers (12)
json
{
    "success": true,
    "response": {
        "status": "success",
        "mensagem": "Foto alterada com sucesso"
    }
}
POST
Obter documentos necessários do cadastro do condutor
https://api-trial.taximachine.com.br/api/integracao/obterDocumentosCadastroCondutor
Retorna todos os documentos necessários para o cadastro de um condutor.

O tipo de identificação, é uma forma de identificação do condutor, desta forma de acordo com o tipo de identificação, o valor da identificação do condutor irá respeitar a regra do tipo enviado.

C: CPF do condutor
V: Viatura do condutor
T: Telefone do condutor
P: Placa do veicúlo do condutor
I: Identificador do condutor
﻿

Body
raw (json)
json
{
    "condutor": {
        "tipo_identificacao": "<char>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Obter documentos necessários
Request
HTTP
POST /api/integracao/obterDocumentosCadastroCondutor HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 105

{
    "condutor": {
        "tipo_identificacao": "I",
        "identificacao": {{entregador_id}}
    }
}
200 OK
Response
Body
Headers (12)
View More
json
{
    "success": true,
    "response": {
        "documentos": [
            {
                "nome": "Alvará de táxi",
                "tipo": "ZG9jXzEy",
                "ativo": true
            },
            {
                "nome": "Certidão de antecedentes criminais",
                "tipo": "ZG9jXzEx",
                "ativo": true
            },
            {
                "nome": "CNH (Carteira Nacional de Habilitação)",
                "tipo": "ZG9jXzg",
                "ativo": false
            },
            {
                "nome": "Comprovante de residência",
                "tipo": "ZG9jXzk",
                "ativo": false
            },
            {
                "nome": "CRLV (Certificado de Registro e Licenciamento do Veículo)",
                "tipo": "ZG9jXzEw",
                "ativo": false
            },
            {
                "nome": "quo consequuntur eligendi",
                "tipo": "ZG9jXzE2OQ",
                "ativo": true
            }
        ],
        "quantidade_documentos": 6
    }
}
POST
Obter documentos cadastrados
https://api-trial.taximachine.com.br/api/integracao/obterDocumentosCondutor
Retorna os documentos cadastrados ao condutor.

O tipo de identificação, é uma forma de identificação do condutor, desta forma de acordo com o tipo de identificação, o valor da identificação do condutor irá respeitar a regra do tipo enviado.

C: CPF do condutor
V: Viatura do condutor
T: Telefone do condutor
P: Placa do veicúlo do condutor
I: Identificador do condutor
﻿

Body
raw (json)
json
{
    "condutor": {
        "tipo_identificacao": "<int>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Obter documentos cadastrados
Request
HTTP
POST /api/integracao/obterDocumentosCondutor HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 105

{
    "condutor": {
        "tipo_identificacao": "I",
        "identificacao": {{entregador_id}}
    }
}
200 OK
Response
Body
Headers (12)
View More
json
{
    "success": true,
    "response": {
        "documentos": [
            {
                "tipo": "ZG9jXzg",
                "nome": "CNH (Carteira Nacional de Habilitação)",
                "url_foto": "{/api/foto?user_id=178&id=793}"
            }
        ],
        "quantidade_documentos": 1
    }
}
Crédito
Atributo	Descrição
tipo_identificacao
I - Id, C - CPF, V - VTR, T - Telefone, P - Placa
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
POST
Recarregar créditos do entregador
https://api-trial.taximachine.com.br/api/integracao/recarregarCreditosCondutor
Os condutores podem possuir carteiras de crédito, com isso, esse endpoint permite adicionar créditos para o condutor em questão.

O tipo de identificação, é uma forma de identificação do condutor, desta forma de acordo com o tipo de identificação, o valor da identificação do condutor irá respeitar a regra do tipo enviado.

C: CPF do condutor
V: Viatura do condutor
T: Telefone do condutor
P: Placa do veicúlo do condutor
I: Identificador do condutor
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Carteira de créditos”.
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (json)
json
{
    "valor": "<float>",
    "observacao": "<string>",
    "condutor": {
        "tipo_identificacao": "<int>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Recarregar créditos
Request
View More
HTTP
POST /api/integracao/recarregarCreditosCondutor HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 192

{
    "valor": 520.25,
    "observacao": "Sed est asperiores voluptates ad voluptatem.",
    "condutor": {
        "tipo_identificacao": "I",
        "identificacao": {{entregador_id}}
    }
}
200 OK
Response
Body
Headers (14)
json
{
    "success": true,
    "response": {
        "registro_id": "616"
    }
}
POST
Sacar créditos do entregador
https://api-trial.taximachine.com.br/api/integracao/sacarCreditosCondutor
Os condutores podem possuir carteiras de crédito, com isso, esse endpoint permite sacar créditos do condutor em questão.

O tipo de identificação, é uma forma de identificação do condutor, desta forma de acordo com o tipo de identificação, o valor da identificação do condutor irá respeitar a regra do tipo enviado.

C: CPF do condutor
V: Viatura do condutor
T: Telefone do condutor
P: Placa do veicúlo do condutor
I: Identificador do condutor
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Carteira de créditos”.
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (json)
json
{
    "valor": "<float>",
    "observacao": "<string>",
    "condutor": {
        "tipo_identificacao": "<char>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Sacar créditos
Request
View More
HTTP
POST /api/integracao/sacarCreditosCondutor HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 205

{
    "valor": 289.76,
    "observacao": "Dolor sint eos eos doloribus eos velit exercitationem et.",
    "condutor": {
        "tipo_identificacao": "I",
        "identificacao": {{entregador_id}}
    }
}
200 OK
Response
Body
Headers (14)
json
{
    "success": true,
    "response": {
        "registro_id": "426"
    }
}
POST
Obter saldo do entregador
https://api-trial.taximachine.com.br/api/integracao/saldoCreditosCondutor
Os condutores podem possuir carteiras de crédito, com isso, esse endpoint permite visualizar o saldo do condutor.

O tipo de identificação, é uma forma de identificação do condutor, desta forma de acordo com o tipo de identificação, o valor da identificação do condutor irá respeitar a regra do tipo enviado.

C: CPF do condutor
V: Viatura do condutor
T: Telefone do condutor
P: Placa do veicúlo do condutor
I: Identificador do condutor
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Carteira de créditos”.
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (json)
json
{
    "condutor": {
        "tipo_identificacao": "<int>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Obter saldo
Request
HTTP
POST /api/integracao/saldoCreditosCondutor HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 105

{
    "condutor": {
        "tipo_identificacao": "I",
        "identificacao": {{entregador_id}}
    }
}
200 OK
Response
Body
Headers (14)
json
{
    "success": true,
    "response": {
        "saldo": 766.81
    }
}
POST
Atualizar entregador
https://api-trial.taximachine.com.br/api/integracao/atualizarCondutor/{{entregador_id}}
Esse endpoint permite a atualização de dados do condutor. São alterados apenas os atributos enviados, os demais atributos não são alterados.

Atributo	Descrição
sexo
M - Masculino, F - Femino
data_nascimento
YYYY-MM-DD
telefone
(0XX) XXXXX-XXXX
vinculo
A - Auxiliar, T - Titular
status_condutor
A - Ativo, G - Aguardando ativação, I - Inativo, S - Suspenso, R - Rejeitado, D - Deletado
veiculo_tipo
B - Bicicleta, C - Carro, M - Moto
placa
dois tipos
cor
ffffff - Branco, c0c0c0 - Prata, ffff00 - Amarelo, 0000cd - Azul, ff8c00 - Laranja, ff0000 - Vermelho, 000000 - Preto, 808080 - Cinza, 00994c - Verde, 964b00 - Marrom, ff69b4 - Rosa, 800080 - Roxo, ffd700 - Dourado, f5f5dc - Bege, 831d1c - Grena, 67a03d - Fantasia
cpf
XXX.XXX.XXX-XX
pagamentos
D - Dinheiro, V - Voucher, T - Ticket, W - Wappa, C - Cartão de crédito, B - Cartão de débito, A - Cartão App, X - Pix, P - PicPay, H - Whatsapp, R - Carteira de créditos, F - Faturado
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Body
raw (json)
View More
json
{
    "id": {{entregador_id}},
    "nome": "Iris Wilderman",
    "sexo": "M",
    "data_nascimento": "2001-01-01",
    "email": "Harold_Rath@example.com",
    "telefone": "(099) 99999-9999",
    "status_condutor": "A",
    "endereco": "Rua Evandro Câmara",
    "numero_endereco": "717",
    "complemento": "Casa",
    "cep": "39402-512",
    "bairro": "Monte Carmelo",
    "cpf": "999.999.999-99",
    "numero_cnh": "99999999999",
    "possui_vinculo": true,
    "vinculo": "T",
    "veiculo_tipo": "M",
    "modelo": "pariatur",
    "placa": "AAA-9999",
    "cor": "ff0000",
    "ano_modelo": "2001",
    "porta_malas_grande": true,
    "adaptado_cadeirante": true,
    "numero_viatura": 451,
    "categorias": [
        "780",
        "459",
        "841"
    ],
    "pagamentos": [
        "V",
        "T",
        "W",
        "C",
        "B",
        "X",
        "P",
        "H",
        "R",
        "F"
    ],
    "exigencias": {
        "veiculo_a_disposicao": false,
        "aceita_encomendas": false,
        "filtro_1": true,
        "filtro_2": true,
        "filtro_3": true,
        "filtro_4": false,
        "filtro_5": true,
        "filtro_6": false
    },
    "informacoes_adicionais": "Ea iste et distinctio voluptatum suscipit.",
    "observacao_interna_1": "Libero minima sint ut at quo enim ratione vitae nesciunt.",
    "observacao_interna_2": "Eos tempore ducimus incidunt et deserunt ad libero.",
    "observacao_interna_3": "Est sint reiciendis et dolorem reprehenderit."
}
Example
200 - Atualizar entregador
Request
View More
HTTP
POST /api/integracao/atualizarTaxista/{{entregador_id}} HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 1383

{
    "id": {{entregador_id}},
    "nome": "Johanna Spinka",
    "sexo": "M",
    "data_nascimento": "2001-01-01",
    "email": "Lurline86@example.net",
    "telefone": "(099) 99999-9999",
    "status_condutor": "A",
    "endereco": "Rua Evandro Câmara",
    "numero_endereco": "717",
    "complemento": "Casa",
    "cep": "39402-512",
    "bairro": "Monte Carmelo",
    "cpf": "999.999.999-99",
    "numero_cnh": "99999999999",
    "possui_vinculo": true,
    "vinculo": "T",
    "veiculo_tipo": "M",
    "modelo": "natus",
    "placa": "AAA-9999",
    "cor": "ff0000",
    "ano_modelo": "2001",
    "porta_malas_grande": true,
    "adaptado_cadeirante": false,
    "numero_viatura": 944,
    "categorias": [
        "603",
        "261",
        "446"
    ],
    "pagamentos": [
        "V",
        "T",
        "W",
        "C",
        "B",
        "X",
        "P",
        "H",
        "R",
        "F"
    ],
    "exigencias": {
        "veiculo_a_disposicao": true,
        "aceita_encomendas": false,
        "filtro_1": false,
        "filtro_2": true,
        "filtro_3": true,
        "filtro_4": false,
        "filtro_5": true,
        "filtro_6": true
    },
    "informacoes_adicionais": "Aliquid ea qui.",
    "observacao_interna_1": "Numquam vel autem optio.",
    "observacao_interna_2": "Ab id et facere.",
    "observacao_interna_3": "Autem aspernatur ullam."
}
200 OK
Response
Body
Headers (12)
json
{
    "success": true,
    "response": {
        "status": "OK",
        "mensagem": "Entregador atualizado com sucesso"
    }
}
GET
Obter entregadores
https://api-trial.taximachine.com.br/api/integracao/condutor
Ao acionar, são retornados todos os condutores da central conforme os parâmetros informados.

Os status do condutor podem ser encontrados, nas seguintes opções:

A: Ativo
G: Aguardando ativação
I: Inativo
S: Suspenso
R: Rejeitado
D: Deletado
Exemplo de Solicitação
Plain Text
GET https://api-trial.taximachine.com.br/api/integracao/condutor?status_condutor=A&pagina=1&limite=5
Exemplo de Resposta
JSON
{
  "success": true,
    "response": [
        {
            "id": "5535",
            "nome": "Nome entregador 1",
            "email": "email1@gaudium.com.br",
            "telefone": "(083) 99420-1743",
            "status": "A",
            "cpf": null,
            "chave_pix": null,
            "pagamentos": [],
            "avaliacao_media": null,
            "data_hora_situacao_cadastral": "2022-06-01 12:35:26",
            "data_hora_ultima_corrida": "2022-06-01 12:36:38",
            "numero_viatura": null,
            "observacao_interna_1": null,
            "observacao_interna_2": null,
            "observacao_interna_3": null,
            "endereco": "",
            "numero_endereco": "",
            "complemento": "",
            "bairro": "",
            "nome_cidade": null,
            "uf_sigla": null,
            "cep": "",
            "pais_nome": null,
            "referencia_endereco": null,
            "dados_extras": ""
        },
        {
            "id": "5536",
            "nome": "Nome entregador 2",
            "email": "email2@gaudium.com.br",
            "telefone": "(022) 99999-4444",
            "status": "A",
            "cpf": "187.294.670-47",
            "chave_pix": "187.294.670-47",
            "pagamentos": [],
            "avaliacao_media": null,
            "data_hora_situacao_cadastral": "2023-11-06 17:44:08",
            "data_hora_ultima_corrida": null,
            "numero_viatura": "12312",
            "observacao_interna_1": null,
            "observacao_interna_2": null,
            "observacao_interna_3": null,
            "endereco": "",
            "numero_endereco": "",
            "complemento": "",
            "bairro": "",
            "nome_cidade": null,
            "uf_sigla": null,
            "cep": "",
            "pais_nome": null,
            "referencia_endereco": "",
            "dados_extras": ""
        },
  ...
  ]
}
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Query Params
id
<int>
ID do condutor que se deseja visualizar as informações. Caso enviado, os demais parâmetros são desconsiderados.

status_condutor
<char>
Retorna apenas os condutores no status desejado. Valores aceitos: Ativo (A), Aguardando ativação (G), Inativo (I), Suspenso (S), Rejeitado (R), Deletado (D).

pagina
<int>
Quantidade de condutores retornados. O limite padrão é 20 e o máximo é 100.

limite
<int>
Qual início da contagem para o limite. O padrão é 1.

telefone
<char>
Telefone do condutor que se deseja visualizar as informações.

Example
200 - Obter entregador
Request
HTTP
GET /api/integracao/condutor?id={{entregador_id}} HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (11)
View More
json
{
    "success": true,
    "response": [
        {
            "id": "315",
            "nome": "Crystal Medhurst",
            "email": "Johanna21@example.com",
            "telefone": "(099) 99999-9999",
            "status": "A",
            "cpf": "999.999.999-99",
            "chave_pix": null,
            "pagamentos": [],
            "avaliacao_media": null,
            "data_hora_situacao_cadastral": "2020-12-28 07:50:54",
            "data_hora_ultima_corrida": null,
            "numero_viatura": "099",
            "observacao_interna_1": null,
            "observacao_interna_2": null,
            "observacao_interna_3": null,
            "endereco": "Zemlak Springs",
            "numero_endereco": "",
            "complemento": "",
            "bairro": "",
            "nome_cidade": "Alainachester",
            "uf_sigla": "",
            "cep": "99999-999",
            "pais_nome": "Cook Islands",
            "referencia_endereco": null,
            "dados_extras": ""
        }
    ]
}
PUT
Atualizar Entregadores
https://api-trial.taximachine.com.br/api/integracao/atualizarCondutores
Esse endpoint permite a atualização em massa dos condutores.

Os dados que deseja atualizar devem ser passados no body, assim como para quais condutores deseja realizar a atualização.

O parâmetro condutores deve ser um array de inteiros, contendo os Ids dos condutores a serem atualizados.

O parâmetro areas_bloqueio deve ser um array de inteiros, contendo os Ids das áreas que deseja atribuir aos condutores.

﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Body
raw (json)
json
{
    "condutores": [315, 98],
    "areas_bloqueio": [850, 141, 17]
}
Example
200 - Sucesso
Request
HTTP
PUT /api/integracaoatualizarCondutores HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: •••••••
Content-Length: 69

{
    "condutores": [16, 636],
    "areas_bloqueio": [584, 146, 79]
}
200 OK
Response
Body
Headers (13)
json
{
    "success": true
}
Empresa
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
Crédito
Atributo	Descrição
tipo_identificacao
I - Id, F - CPF, J - CNPJ, T - Telefone, C - Número de contrato
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
POST
Recarregar créditos da empresa
https://api-trial.taximachine.com.br/api/integracao/recarregarCreditosEmpresa
As empresas podem possuir carteiras de crédito, com isso, esse endpoint permite adicionar créditos para a empresa em questão.

O tipo de identificação, é uma forma de identificação da empresa, desta forma de acordo com o tipo de identificação, o valor da identificação da empresa irá respeitar a regra do tipo enviado.

C: CPF da empresa
J: CNPJ da empresa
T: Telefone do condutor
C: Número do contrato
I: Identificador da empresa
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Carteira de créditos”.
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (json)
json
{
    "valor": "<float>",
    "observacao": "<string>",
    "empresa": {
        "tipo_identificacao": "<char>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Recarregar créditos
Request
View More
HTTP
POST /api/integracao/recarregarCreditosEmpresa HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 193

{
    "valor": 810.93,
    "observacao": "Error quos debitis temporibus commodi blanditiis.",
    "empresa": {
        "tipo_identificacao": "I",
        "identificacao": {{empresa_id}}
    }
}
200 OK
Response
Body
Headers (15)
json
{
    "success": true,
    "response": {
        "registro_id": "896"
    }
}
POST
Sacar créditos da empresa
https://api-trial.taximachine.com.br/api/integracao/sacarCreditosEmpresa
As empresas podem possuir carteiras de crédito, com isso, esse endpoint permite sacar créditos para a empresa em questão.

O tipo de identificação, é uma forma de identificação da empresa, desta forma de acordo com o tipo de identificação, o valor da identificação da empresa irá respeitar a regra do tipo enviado.

C: CPF da empresa
J: CNPJ da empresa
T: Telefone do condutor
C: Número do contrato
I: Identificador da empresa
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Carteira de créditos”.
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (json)
json
{
    "valor": "<float>",
    "observacao": "<string>",
    "empresa": {
        "tipo_identificacao": "<char>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Sacar créditos
Request
View More
HTTP
POST /api/integracao/sacarCreditosEmpresa HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 168

{
    "valor": 927.98,
    "observacao": "Inventore error non qui.",
    "empresa": {
        "tipo_identificacao": "I",
        "identificacao": {{empresa_id}}
    }
}
200 OK
Response
Body
Headers (14)
json
{
    "success": true,
    "response": {
        "registro_id": "429"
    }
}
POST
Obter saldo da empresa
https://api-trial.taximachine.com.br/api/integracao/saldoCreditosEmpresa
As empresas podem possuir carteiras de crédito, com isso, esse endpoint permite verificar o saldo em créditos para a empresa em questão.

O tipo de identificação, é uma forma de identificação da empresa, desta forma de acordo com o tipo de identificação, o valor da identificação da empresa irá respeitar a regra do tipo enviado.

C: CPF da empresa
J: CNPJ da empresa
T: Telefone do condutor
C: Número do contrato
I: Identificador da empresa
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Carteira de créditos”.
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (json)
json
{
    "empresa": {
        "tipo_identificacao": "<int>",
        "identificacao": "<string><int>"
    }
}
Example
200 - Obter saldo
Request
HTTP
POST /api/integracao/saldoCreditosEmpresa HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 101

{
    "empresa": {
        "tipo_identificacao": "I",
        "identificacao": {{empresa_id}}
    }
}
200 OK
Response
Body
Headers (14)
json
{
    "success": true,
    "response": {
        "saldo": 440.71
    }
}
GET
Obter empresas
https://api-trial.taximachine.com.br/api/integracao/empresa
Retorna todas as empresas conveniadas à central, podendo também retornar os dados de uma empresa específica, ou a do usuário, caso seja um usuário da empresa.

O campo "dados_extras" somente é retornado com autenticação de Central. Caso uma quebra de linha ocorra, serão retornados os caracteres "\r\n" indicando a quebra de linha.

Para ter acesso ao endpoint o usuário autenticado deve ter a permissão “API - Empresa”.
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Query Params
empresa_id
<int>
Id da empresa a ser obtida. Se a autenticação for de uma empresa, terá como resposta os dados da empresa e o parâmetro é ignorado

limite
<int>
Quantidade de empresas retornadas. O limite padrão é 20 e o máximo é 100.

pagina
<int>
Qual início da contagem para o limite. O padrão é 1.

Example
200 - Obter empresas
Request
HTTP
GET /api/integracao/empresa HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (12)
View More
json
{
    "success": true,
    "response": [
        {
            "id": "588",
            "nome": "Mertz, Buckridge and Grady",
            "numero_contrato": "527",
            "endereco": "Rua 32",
            "complemento": null,
            "bairro": "Centro",
            "cidade": "Barretos",
            "uf": "SP",
            "cep": "14783-215",
            "lat": "-20.556480000",
            "lng": "-48.577464800",
            "telefone": "265-996-5641",
            "status_empresa": "A",
            "data_hora_cadastro": "2024-07-21 12:15:00",
            "dados_extras": "Dados extras 1\r\nDados extras 2",
            "tipo_documento": "CPF",
            "documento": "xxx.xxx.xxx-xx",
            "tipos_pagamento": [
                "B",
                "C"
            ],
            "categorias": [
                {
                "id": "72",
                "nome": "Categoria1"
                },
                {
                "id": "94",
                "nome": "Categoria2"
                }
            ]
        },
        {
            "id": "270",
            "nome": "Empresa Deletada",
            "numero_contrato": null,
            "endereco": null,
            "complemento": null,
            "bairro": null,
            "cidade": null,
            "uf": null,
            "cep": null,
            "lat": null,
            "lng": null,
            "telefone": null,
            "status_empresa": "D",
            "data_hora_cadastro": "2023-08-10 14:20:00",
            "dados_extras": null,
            "tipo_documento": null,
            "documento": null,
            "tipos_pagamento": [],
            "categorias": []
        },
        {
            "id": "{{randomInt}}",
            "nome": "Becker, Rosenbaum and Gleichner",
            "numero_contrato": "{{randomInt}}",
            "endereco": "Rua Exemplo 2, 18",
            "complemento": "Faixa amarela",
            "bairro": "Bairro Exemplo",
            "cidade": "Patos",
            "uf": "PB",
            "cep": "xxxxx-xxx",
            "lat": "-22.907994",
            "lng": "-43.184431",
            "telefone": "549-518-5594",
            "status_empresa": "S",
            "data_hora_cadastro": "2024-07-21 12:13:14",
            "dados_extras": "Dados extras 1\r\nDados extras 2",
            "tipo_documento": "CNPJ",
            "documento": "xx.xxx.xxx/0001-xx",
            "tipos_pagamento": [
                "D",
                "B",
                "C",
                "F",
                "X",
                "P",
                "H",
                "R"
            ],
            "categorias": [
                {
                "id": "72",
                "nome": "Categoria1"
                },
                {
                "id": "86",
                "nome": "Categoria2"
                }
            ],
            "admins": [
                {
                    "nome": "Lillian45",
                    "email": "Marisol58@example.net"
                }
            ]
        }
    ]
}
PUT
Atualizar Empresa
https://api-trial.taximachine.com.br/api/integracao/atualizarEmpresa/{{empresa_id}}
Esse endpoint permite a atualização de dados da empresa (status ou número de contrato), sendo necessário informar o ID da empresa que se deseja atualizar no final da URL.

Devem ser passados no body os dados que se deseja atualizar.

Permitidos para serem atualizados:

status_empresa
numero_contrato
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão “API - Empresa”.
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Query Params
empresa_id
<int>
Id da empresa a ser obtida. Se a autenticação for de uma empresa, terá como resposta os dados da empresa e o parâmetro é ignorado

Body
raw (json)
json
{
    "status_empresa" : "A",
    "numero_contrato": 997102
}
Example
200 - Atualizar Empresa (status e número do contrato)
Request
HTTP
PUT /api/integracao/atualizarEmpresa/{{empresa_id}} HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 61

{
    "status_empresa" : "G",
    "numero_contrato": 997102
}
200 OK
Response
Body
Headers (10)
json
{
    "success": true,
    "response": {
        "status": "OK",
        "mensagem": "Empresa atualizada com sucesso"
    }
}
PUT
Atualizar Empresas
https://api-trial.taximachine.com.br/api/integracao/atualizarEmpresas
Esse endpoint permite a atualização de empresas em massa.

Os dados que deseja atualizar devem ser passados no body, assim como para quais empresas deseja realizar a atualização.

O parâmetro empresas deve ser um array de inteiros, contendo os Ids das empresas a serem atualizadas.

O status_empresa deve ser uma string, tendo como possíveis valores:

A - Ativo
S - Suspenso
G - Aguardando ativação
O parâmetro categorias deve ser um array de inteiros, contendo os Ids das categorias que deseja utilizar para as empresas.

O parâmetro tipos_pagamento deve ser um array de strings, contendo as siglas dos tipos de pagamento que deseja utilizar para as empresas, tendo como possíveis valores:

B: Débito (máquina)
C: Crédito (máquina)
D: Dinheiro
F: Faturado
H: Whatsapp
P: Picpay
R: Carteira de Créditos
X: Pix
O parâmetro area_atuacao_empresa_id deve ser um inteiro, contendo o Id da área de atuação que deseja atualizar. Para saber o Id de cada área disponível, basta acessar o endpoint /listarAreasAtuacaoEmpresa.

Para ter acesso ao endpoint o usuário autenticado deve ter a permissão “API - Empresa”.
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Body
raw (json)
json
{
    "empresas":[330, 463],
    "status_empresa": "A",
    "categorias": [194, 902],
    "tipos_pagamento": ["D", "C"],
    "area_atuacao_empresa_id": 143
}
Example
200 - Atualizar Empresas
Request
View More
HTTP
PUT /api/integracao/atualizarEmpresas HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 148

{
    "empresas":[55],
    "status_empresa": "A",
    "categorias": [71, 83],
    "tipos_pagamento": ["D", "C"],
    "area_atuacao_empresa_id": 45
}
200 OK
Response
Body
Headers (12)
json
{
    "success": true
}
POST
Cadastrar Empresa
https://api-trial.taximachine.com.br/api/integracao/cadastrarEmpresa
Este endpoint permite o cadastro de empresas.

Devem ser passados os dados documento (número documento) e tipo_documento (CPF ou CNPJ).

Indicar número de contrato e nome fantasia como no site.

Dados de endereço e telefone como no site.

A situacao_cadastral deve ser (A - Ativo, G - Aguardando ativação ou S - Suspenso).

Categorias deve ser um array de inteiros indicando o id da categoria que deseja disponibilizar para empresa. Um array vazio ([]) significa todas as categorias.

Tipos de pagamento deve ser um array de string contendo a sigla de algum dos tipos de pagamento abaixo. Um array vazio ([]) significa todos os tipos de pagamento.

B: Débito (máquina)
C: Crédito (máquina)
D: Dinheiro
F: Faturado
H: Whatsapp
P: Picpay
R: Carteira de Créditos
X: Pix
O parâmetro area_atuacao_empresa_id deve ser um inteiro, contendo o Id da área de atuação que deseja atualizar. Para saber o Id de cada área disponível, basta acessar o endpoint /listarAreasAtuacaoEmpresa. Caso o parâmetro não seja passado na requisição, o cadastro será feito utilizando a área padrão da bandeira.

Indicar se deve cobrar retorno (booleano).

Indicar se deve obrigar finalização com retorno pela empresa (booleano).

Indicar se deve habilitar solicitação rápida (booleano) e se sim, indicar qual categoria (deve estar presente no array de categorias acima, caso o array de categorias for vazio, apenas deve ser uma válida) e qual tipo de pagamento (conforme descrição acima).

Indicar observação se tiver (passar null caso contrário).

Indicar dados extras se tiver (passar null caso contrário).

Para ter acesso ao endpoint o usuário autenticado deve ter a permissão “API - Empresa”.
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Body
raw (json)
View More
json
{
    "documento": "57.268.792/0001-05",
    "tipo_documento": "CNPJ", // ou CPF
    "numero_contrato": "104896",
    "razao_social": "Razão social nova empresa",
    "nome_fantasia": "Nome nova empresa",
    "endereco": {
        "logradouro": "Rua Dorval Porto",
        "complemento": null,
        "uf": "AM", // SP, RJ, PB, PE, RN, ...
        "cidade": "Barcelos",
        "bairro": "Centro",
        "cep": "CEP nova empresa"
    },
    "telefone": {
        "ddd": "85",
        "numero": "99999-8888"
    },
    "situacao_cadastral": "S", // A S G
    "categorias": [86],
    "tipos_pagamento": ["B", "C", "D", "F", "H", "P", "R", "X"],
    "area_atuacao_empresa_id": 45,
    "cobrar_retorno": true,
    "obrigar_finalizacao_com_retorno_pela_empresa": false,
    "solicitacao_rapida": {
        "habilitar": true,
        "categoria": 86,
        "tipo_pagamento": "D"
    },
    "observacao_condutor": "Obs",
    "dados_extras": "Dados"
}
Example
200 - Cadastrar Empresa
Request
View More
HTTP
POST /api/integracao/cadastrarEmpresa HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 943

{
    "documento": "57.268.792/0001-05",
    "tipo_documento": "doc", // ou CPF
    "numero_contrato": "104896",
    "razao_social": "Razão social nova empresa",
    "nome_fantasia": "Nome nova empresa",
    "endereco": {
        "logradouro": "Rua Dorval Porto",
        "complemento": null,
        "uf": "AM", // SP, RJ, PB, PE, RN
        "cidade": "Barcelos",
        "bairro": "Centro",
        "cep": "CEP nova empresa"
    },
    "telefone": {
        "ddd": "85",
        "numero": "99999-8888"
    },
    "situacao_cadastral": "S", // A S G
    "categorias": [86],
    "tipos_pagamento": ["B", "C", "D", "F", "H", "P", "R", "X"],
    "area_atuacao_empresa_id": 45,
    "cobrar_retorno": true,
    "obrigar_finalizacao_com_retorno_pela_empresa": false,
    "solicitacao_rapida": {
        "habilitar": true,
        "categoria": 86,
        "tipo_pagamento": "D"
    },
    "observacao_condutor": "Obs",
    "dados_extras": "Dados"
}
200 OK
Response
Body
Headers (10)
json
{
    "success": true,
    "response": {
        "status": "OK",
        "mensagem": "Empresa cadastrada com sucesso."
    }
}
GET
Obter áreas de atuação
https://api-trial.taximachine.com.br/api/integracao/listarAreasAtuacaoEmpresa
Esse endpoint retorna as áreas de atuação de empresa da central. Serão retornados os seguintes dados de cada área:

id - Identificador da área
nome- Nome da área
padrao - Indica se a área é a padrão da central
Para ter acesso ao endpoint o usuário autenticado deve ter a permissão “API - Empresa”.
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Example
200 - Obter áreas de atuação
Request
HTTP
GET /api/integracao/listarAreasAtuacaoEmpresa HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (10)
View More
json
[
    {
        "id": 38,
        "nome": "Área 1",
        "padrao": true
    },
    {
        "id": 41,
        "nome": "Área 2",
        "padrao": false
    },
    {
        "id": 42,
        "nome": "Área 3",
        "padrao": false
    },
    {
        "id": 43,
        "nome": "Área 4",
        "padrao": false
    },
    {
        "id": 44,
        "nome": "Área 5",
        "padrao": false
    },
    {
        "id": 45,
        "nome": "Área 6",
        "padrao": false
    },
    {
        "id": 105,
        "nome": "Área 7",
        "padrao": false
    }
]
Solicitação
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
Programada
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
GET
Consultar programada
https://api-trial.taximachine.com.br/api/integracao/consultarProgramada
Consultar Programadas
Esta solicitação é usada para obter uma única programada caso seja passada o id e caso não seja passada e retornado um conjunto de programadas.

Exemplo de Solicitação
Plain Text
GET https://api-trial.taximachine.com.br/api/integracao/consultarProgramada?id_mch_programada=465&pagina=79&limite=306
Exemplo de Resposta com id
JSON
{
  "success": true,
    "response": {
    "situacao": "A",
    "situacao_formatada": "Aguardando Distribuição",
    "data_previsao_disparo": "05/09/2023",
    "hora_previsao_disparo": "15:59",
    "id_mch": null,
    "empresa": {
        "id": "419",
        "nome": "empresa_nome"
    }
  }
}
Exemplo de Resposta sem id
JSON
{
  "success": true,
    "response": [
        {
            "id_mch_programada": "1394",
            "situacao": "Aguardando Distribuição",
            "situacao_formatada": "12/12/2023 17:32:18",
            "data_previsao_disparo": "12/12/2023",
            "hora_previsao_disparo": "17:32:18",
            "id_mch": null,
            "empresa": {
                "id": "641",
                "nome": "empresa_nome"
            }
        },
        {
            "id_mch_programada": "1393",
            "situacao": "Cancelada",
            "situacao_formatada": "26/01/2021 01:50:00",
            "data_previsao_disparo": "26/01/2021",
            "hora_previsao_disparo": "01:50:00",
            "id_mch": null,
            "empresa": {
                "id": null,
                "nome": null
            }
        },
        {
            "id_mch_programada": "1392",
            "situacao": "Distribuída",
            "situacao_formatada": "21/01/2021 00:55:00",
            "data_previsao_disparo": "21/01/2021",
            "hora_previsao_disparo": "00:55:00",
            "id_mch": "100003594",
            "empresa": {
                "id": "220",
                "nome": "empresa_nome"
            }
        },
  ...
  ]
}
Resposta:
Situação	Situação formatada
A
Aguardando Distribuição
D
Distribuída
C
Cancelada
G
Erro na Distribuição
Outros
---
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Query Params
id_mch_programada
<int>
(Required) Número da O.S programada

Example
200 - Consultar programada
Request
HTTP
GET /api/integracao/consultarProgramada?id_mch_programada=680 HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (12)
View More
json
{
    "success": true,
    "response": {
        "situacao": "D",
        "situacao_formatada": "Distribuída",
        "data_previsao_disparo": "18/07/2018",
        "hora_previsao_disparo": "15:11",
        "id_mch": null,
        "empresa": {
            "id": "194",
            "nome": "empresa_nome"
        }
    }
}
POST
Cancelar programada
https://api-trial.taximachine.com.br/api/integracao/cancelarProgramada
Cancela (mudando para status C), a solicitação programada informada. A solicitação não pode estar com o status aguardando (A).

Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Entrega”.
﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Body
raw (text)
text
{
    "id_mch_programada": "<int>"
}
Example
200 - Cancelar programada
Request
HTTP
POST /api/integracao/cancelarProgramada HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
Content-Length: 33

{
    "id_mch_programada": 5642
}
200 OK
Response
Body
Headers (12)
json
{
    "success": true,
    "response": {
        "id_mch_programada": 5642,
        "mensagem": "Programada cancelada com sucesso"
    }
}
Entregador
﻿

Authorization
Basic Auth
This folder is using an authorization helper from collection Documentação Machine - Entregas
GET
Obter posição do entregador
https://api-trial.taximachine.com.br/api/integracao/posicaoCondutor
O retorno será a latitude e longitude do condutor no instante. Caso a entrega ainda estiver na fase de despacho (status distribuindo, pendente ou aguardando aceite) ou já estiver sido finalizada/cancelada (status não atendida, cancelada ou finalizada), o retorno será laitude e longitude null.

﻿

Authorization
Basic Auth
This request is using an authorization helper from collection Documentação Machine - Entregas
Query Params
id_mch
<int>
(Required) Número da O.S

Example
200 - Obter posição do entregador
Request
HTTP
GET /api/integracao/posicaoCondutor?id_mch=123 HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (12)
json
{
    "success": true,
    "response": {
        "lat_condutor": "17.0365",
        "lng_condutor": "55.8272"
    }
}
GET
Estimar solicitação
https://api-trial.taximachine.com.br/api/integracao/estimarSolicitacao?lat_partida=-19.4677545&lng_partida=-42.5752169&lat_desejado=-19.473268&lng_desejado=-42.5076436
Permite obter a estimativa do valor da solicitação em uma única categoria.

Para ter acesso ao endpoint o usuário autenticado deve ter a permissão de “API - Entrega”.
﻿

Authorization
Basic Auth
Username
suporte@atendeloja.com.br
Password
605622
Query Params
endereco_partida
<string>
(Required) Endereço do local de partida

bairro_partida
<string>
(Required) Bairro do local de partida

cidade_partida
<string>
(Required) Cidade do local de partida

estado_partida
<string>
(Required) Sigla do estado do local de partida

lat_partida
-19.4677545
Latitude do local de partida

lng_partida
-42.5752169
Longitude do local de partida

endereco_desejado
<string>
(Required) Endereço do local desejado

bairro_desejado
<string>
(Required) Bairro do local desejado

cidade_desejado
<string>
(Required) Cidade do local desejado

estado_desejado
<string>
(Required) Sigla do estado do local desejado

lat_desejado
-19.473268
Latitude do local desejado

lng_desejado
-42.5076436
Longitude do local desejado

latlng_paradas
<string>
Latitude e longitude das paradas. Cada parada deve conter o separador |

categoria_id
<int>
Identificação da categoria

categoria_nome
<string>
Nome da categoria

data
<data>
Data da entrega programada. Formato YYYY-MM-DD

hora
<hora>
Hora da entrega programada. Formato HH:MM:SS

com_retorno
<bool>
Indica se a solictação irá ter retorno ao local de coleta

Example
200 - Estimar solicitação por localização
Request
View More
HTTP
GET /api/integracao/estimarSolicitacao?endereco_partida=Rua Evandro Câmara, 717&bairro_partida=Monte Carmelo&cidade_partida=Montes Claros&estado_partida=MG&endereco_desejado=Aeroporto de Montes Claros - Mário Ribeiro&bairro_desejado=Jaraguá&cidade_desejado=Montes Claros&estado_desejado=MG HTTP/1.1
Host: api-trial.taximachine.com.br
api-key: mch_api_5FwFRzkPJDhRkMLxTslOgde7
200 OK
Response
Body
Headers (12)
View More
json
{
    "success": true,
    "response": {
        "estimativa_valor": 870.22,
        "estimativa_minutos": 7,
        "estimativa_km": 4.05,
        "categoria_nome": "fugit",
        "tarifa_nome": "facere",
        "partida": {
            "lat": -16.7177506,
            "lng": -43.8340907
        },
        "desejado": {
            "lat": -16.7049531,
            "lng": -43.8199862
        }
    }
}
