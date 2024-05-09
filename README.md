# Sistema Bancário - Desafio 2 - Bootcamp Backend com Python - DIO

Bem-vindo ao repositório do **Sistema Bancário - Desafio 2** do Bootcamp Backend com Python promovido pela Digital Innovation One (DIO). Este repositório contém um sistema bancário que permite operações como depósito, saque, extrato, bem como a criação de usuários e contas correntes.

## Requisitos do Desafio

O desafio exigiu aprimorar o sistema bancário do [Desafio 1](https://github.com/gui-brito14/python_desafio_dio_sistema_bancario) com os seguintes requisitos:

- **Funções específicas para operações bancárias:** Depósito, Saque e Extrato.
  - A função `saque` deve receber parâmetros apenas por nome (keyword-only).
  - A função `depósito` deve receber parâmetros apenas por posição (positional-only).
  - A função `extrato` pode receber parâmetros de ambas as formas.
- **Funções adicionais para gerenciamento de usuários e contas correntes:**
  - A função `criar_usuario` armazena usuários em listas contendo nome, data de nascimento, endereço (logradouro, bairro, cidade, estado), e CPF (apenas números, sem duplicatas).
  - A função `criar_conta_corrente` cria contas correntes associadas a usuários, com uma agência, um número de conta sequencial e um proprietário (usuário). Um usuário pode ter várias contas, mas uma conta é associada a apenas um usuário.
- **Outras melhorias:**
  - Uma função para listar usuários e contas existentes.
  - Um menu para escolher a conta antes de realizar operações bancárias, garantindo que as operações afetem apenas a conta selecionada.
  - Otimizações para um sistema mais robusto e flexível.

## Funcionalidades do Sistema

O sistema bancário agora permite o seguinte:

- **Criar Usuários:** Adicione usuários ao sistema com informações como nome, data de nascimento, endereço completo e CPF. O CPF deve ser único.
- **Criar Contas Correntes:** Crie contas correntes associadas a usuários. Cada conta tem um número sequencial único e uma agência padrão.
- **Operações Bancárias:** Realize operações como depósito, saque e extrato em contas específicas.
- **Listar Usuários e Contas:** Veja uma lista de todos os usuários e contas cadastradas no sistema.

## Como Usar

1. **Criação de Usuários:** Use a função `criar_usuario` para adicionar usuários ao sistema.
2. **Criação de Contas Correntes:** Use a função `criar_conta_corrente` para criar contas para os usuários existentes.
3. **Seleção de Conta:** Antes de realizar operações, selecione uma conta existente para garantir que as operações afetem a conta correta.
4. **Operações Bancárias:** Use as funções `depósito`, `saque` e `extrato` para interagir com a conta selecionada.
5. **Listar Usuários e Contas:** Verifique os usuários e contas cadastrados usando a função `listar_usuarios` e `listar_contas`.

## Contribuição

Se deseja contribuir para este projeto, por favor, envie um pull request ou crie uma issue para discutir suas ideias. Feedback e sugestões são sempre bem-vindos!

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE).

## Agradecimentos

Agradecemos à DIO pela oportunidade e suporte neste bootcamp. Este projeto faz parte do aprendizado no processo de aprimoramento em Backend com Python.

