# Documentação para Requisições à Rota de Download

A rota `/downloads` fornece a funcionalidade de download de arquivos. Certifique-se de seguir as instruções abaixo para fazer requisições corretas.

### Localização dos Arquivos para Download

Os arquivos disponíveis para download estão armazenados no servidor `sigmasoftware.com.br`, dentro do diretório `httpdocs`. Ao fazer uma requisição para a rota de download, certifique-se de fornecer o caminho correto para o arquivo desejado dentro desse diretório.

## Autenticação

Antes de fazer qualquer requisição, você precisa incluir um token de autenticação válido no cabeçalho `Authorization`.

- **Formato do Token:** `Bearer <seu_token_secreto>`

## Requisição para Download de Arquivo

**Método:** GET

**Endpoint:** `https://www.sigmasoftware.com.br/ws/downloads/?file=`

### Parâmetros da URL

- **`file` (QueryString):** Nome do arquivo a ser baixado.

### Exemplo de Requisição (cURL)

```bash
curl -H "Authorization: Bearer seu_token_secreto" https://www.sigmasoftware.com.br/ws/downloads/?file=sigmaclientelib.ini
````

## Respostas

- **Sucesso (Código de Status 200):** O arquivo será baixado.

- **Erro de Autenticação (Código de Status 401):** Se o token fornecido for inválido.

Exemplo de resposta:

```json
{
  "message": "Autenticação falhou!"
}
````

- **Nenhum arquivo passado (Código de Status 404):** Se não for passado o nome do arquivo pela url.

Exemplo de resposta:

```json
{
  "message": "Nenhum arquivo informado!"
}
````

- **Arquivo não existe (Código de Status 404):** Se for passado um arquivo que não existe no servidor.

Exemplo de resposta:

```json
{
  "message": "Arquivo não encontrado!"
}
````
