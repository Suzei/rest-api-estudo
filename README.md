# REST API - Estudo

## Recursos

- Alteração de Estado: Quando algo é alterado na API/ Quando um dado é criado

- Alinhamento lógico entre as entidades, contento base paths e caminhos

- Padrões para requisitar e montar uma API Rest:

  • Usar substantivos para se referir aos dados ou parâmetros (Ex: carrinho, banco, lugar)

  • Usar sempre plurais para se definir a grupos, pois uma API se dá por grupos (Ex: clientes, vendas)

  • Versionar o contrato de API (v1, v2, etc) depois do base path;

  • Manter sempre uma ordem hierárquica (ordens/18789/produtos) <- ordens contem produtos, sempre analisar dentro da API o que vem primeiro, pra não ficar tudo muito bagunçado.

  • Usar a case que a empresa utiliza (camelCase, snake_case, kebab-case, PascalCase)

  • Utilizar api no início dos domínios, para manipular API e fazer uma separação do domínio principal.

## Verbos

- Os verbos em HTTP são classificados em dois: seguros e idempotentes

  • Seguros : Não causa alteração de estado em um servidor

  • Idempotentes: Posso chamar esse verbo, pois independente das mudanças, esse verbo terá o mesmo resultado

- Existem vários verbos que podem ser usados em uma requisição, mas estes são os mais comuns:

• POST - Cria estados - POSTAR/CRIAR

- Inseguro - Altera o estado criando estados novos
- Não é idempotente - Será diferente em cada requisição, não será um valor constante
- Não usa cache

• GET - Consulta estados - PEGAR/CONSULTAR

- Seguro - É possível fazer várias chamadas GET sem alterar o estado de nenhuma instância
- Idempotente - Irá obter a mesma resposta, pois está consultando dados. É mais aceitável cache por estar retornando a mesma resposta várias vezes em uma solicitação

• PUT - Substituição de estados (geralmente criando eles se não houver) - POR/COLOCAR

- Inseguro: Altera o estado do servidor, adicionando novos dados
- Idempotente: Causa a mesma alteração de estado, uma constante de criação e/ou substituição
- Não usa cache - Não tem característica de consulta

• PATCH - Alteração parcial ou singular de um estado (basicamente atualiza um dado) ATUALIZAR

- Inseguro: Altera o estado do servidor(modifica os dados)
- Idempotente: Retorna o mesmo tipo de substituição várias vezes
- Não usa cache - Não tem característica de consulta

• DELETE - Apaga um ou mais recursos de uma instância - DELETAR/EXCLUIR

- Inseguro: Altera o estado (deletando os dados)
- Idempotente: Sua função é sempre remover instâncias, ou seja, sua finalidade é constante
- Não usa cache: Não tem característica de consulta

{
Resumo sobre verbos:

Em exceção de um, todos os verbos são inseguros, pois sempre vão alterar estados dentro de um recurso. A exceção é o GET, que não irá alterar em nada por ser de cunho consultivo.

Todos são idempotentes, menos o POST. Isso por quê o restante sempre irá ter um valor igual ou terá uma funcionalidade que não muda, mesmo sendo chamado várias vezes.

Apenas o GET usa cache para armazenar na memória. Os outros não necessitam de cache por quê manipulam e alteram dados constantemente em suas chamadas(são inseguros.)
}

# Códigos HTTP

Números que identificam algum tipo de operação no protocolo HTTP

São divididos em 5 - 1xx, 2xx, 3xx, 4xx e 5xx

• 2xx - Sucesso em operações

- 200 - OK (Requisição foi um sucesso)
- 201 - CREATED - (Uma nova instância foi criada) / POST OU PUT
- 202 - ACCEPTED - (O recurso será atualizado de forma assíncrona)
- 204 - NO CONTENT - A requisição foi processada / DELETE retorna isso
- 206 - PARTIAL CONTENT - (Paginação quando há muitos itens)

• 4xx - Erro no client side

- 400 - BAD REQUEST - (Campo digitado errado, uma informação obrigatória não preenchida)
- 401 - UNAUTHORIZED - (Credenciais inválidas, senha errada, CPF errado)
- 403 - FORBIDDEN - (Credenciais válidas, mas o recurso não está autorizado)
- 404 - NOT FOUND - (Quando uma URL não existe ou está digitada de forma errada)
- 410 - GONE - (Quando o recurso na URL não existe)
- 422 - Unprocessable Entity - (Quando as informações estão certas, mas um condicional impede aquilo de ser enviado)

• 5xx - Erro no server side

- 500 - INTERNAL SERVER ERROR - (Quando há erro no servidor, de forma interna)
- 503 - SERVICE UNAVAILABLE - (Quando é um erro temporário)
- 504 - GATEWAY TIMEOUT - (Quando uma aplicação tá lenta)
