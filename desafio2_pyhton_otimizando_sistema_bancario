# Menu principal com mais opções
main_menu = """
[1] Fazer operações bancárias
[2] Registrar novo usuário
[3] Registrar nova conta bancária
[4] Listar usuários
[5] Listar contas bancárias
[6] Sair

=> """

# Menu para operações bancárias
banking_menu = """
[1] Depósito
[2] Saque
[3] Extrato
[4] Alterar Limite
[5] Voltar ao Menu Principal

=> """

# Dados do sistema bancário
usuarios = []  # Lista de usuários
contas = []  # Lista de contas bancárias
contador_contas = 1  # Contador para números de contas

import re

def registrar_usuario(usuarios):
    nome = input("Digite nome e sobrenome: ")
    
    # Verifica se há um espaço no nome
    if " " not in nome:
        print("Erro: Nome deve conter pelo menos um espaço para nome e sobrenome.")
        return

    data_nascimento = input("Digite data de nascimento (dd/mm/aaaa): ")

    # Verifica se a data de nascimento está no formato correto
    if not re.match(r"^\d{2}/\d{2}/\d{4}$", data_nascimento):
        print("Erro: Data de nascimento deve seguir o padrão dd/mm/aaaa.")
        return

    cpf = input("Digite CPF (apenas números): ")

    # Verifica se o CPF tem exatamente 11 dígitos e contém apenas números
    if not (len(cpf) == 11 and cpf.isdigit()):
        print("Erro: CPF deve ter 11 dígitos e conter apenas números.")
        return

    rua = input("Digite o logradouro: ")
    numero = input("Digite o número: ")
    bairro = input("Digite o bairro: ")
    cidade = input("Digite a cidade: ")
    estado = input("Digite a sigla do estado: ")

    # Verifica se o estado tem exatamente dois caracteres e está em maiúsculas
    if not (len(estado) == 2 and estado.isupper()):
        print("Erro: A sigla do estado deve conter dois caracteres maiúsculos.")
        return

    endereco = {
        "rua": rua,
        "numero": numero,
        "bairro": bairro,
        "cidade": cidade,
        "estado": estado,
    }

    # Verifica se o CPF já está registrado
    if any(u["cpf"] == cpf for u in usuarios):
        print("Erro: CPF já registrado. Registro de usuário falhou.")
        return

    novo_usuario = {"nome": nome, "data_nascimento": data_nascimento, "cpf": cpf, "endereco": endereco}
    usuarios.append(novo_usuario)

    print("Usuário registrado com sucesso.")

# Função para registrar uma nova conta bancária
contador_contas = 1
def registrar_conta_bancaria(usuarios, contas):
    global contador_contas
    cpf = input("Digite o CPF do usuário para esta conta (apenas números): ")

    usuario = next((u for u in usuarios if u["cpf"] == cpf), None)

    if not usuario:
        print("Usuário com esse CPF não encontrado. Registro da conta falhou.")
        return

    nova_conta = {
        "numero_conta": contador_contas,
        "agencia": "0001",
        "proprietario": usuario,
        "saldo": 0,
        "limite": 500,
        "extrato": "",
        "contagem_saques": 0,
        "LIMITE_SAQUES": 3,
        "total_sacado": 0,
    }

    contas.append(nova_conta)
    contador_contas += 1

    print("Conta bancária registrada com sucesso.")

# Função para listar usuários
def listar_usuarios(usuarios):
    if not usuarios:
        print("Nenhum usuário registrado.")
    else:
        for usuario in usuarios:
            print(f"Nome: {usuario['nome']}, CPF: {usuario['cpf']}, Endereço: {usuario['endereco']}")

# Função para listar contas bancárias
def listar_contas(contas):
    if not contas:
        print("Nenhuma conta registrada.")
    else:
        for conta in contas:
            print(f"Número da Conta: {conta['numero_conta']}, Agência: {conta['agencia']}, Proprietário: {conta['proprietario']['nome']}")

# Função para selecionar um usuário pelo CPF
def selecionar_usuario_por_cpf(usuarios, cpf):
    return next((u for u in usuarios if u["cpf"] == cpf), None)

# Função para selecionar uma conta para um usuário
def selecionar_conta_por_usuario(usuario, contas):
    contas_do_usuario = [conta for conta in contas if conta["proprietario"]["cpf"] == usuario["cpf"]]

    if len(contas_do_usuario) == 1:
        return contas_do_usuario[0]  # Se houver apenas uma conta, retorna ela

    # Se houver mais de uma conta, peça ao usuário para selecionar
    if len(contas_do_usuario) > 1:
        print("Selecione a conta para operar:")
        for idx, conta in enumerate(contas_do_usuario):
            print(f"[{idx + 1}] Conta número: {conta['numero_conta']}, Agência: {conta['agencia']}")

        opcao = int(input("=> ")) - 1
        
        if opcao >= 0 and opcao < len(contas_do_usuario):
            return contas_do_usuario[opcao]

    return None

# Função para depósito (posicional apenas)
def deposito(saldo, valor):
    if valor > 0:
        saldo += valor
        extrato = f"\nDepósito: R$ {valor:.2f}\n"
        return saldo, extrato
    else:
        return saldo, "Valor de depósito inválido."

# Função para saque (apenas por palavras-chave)
def saque(*, saldo, limite, contagem_saques, LIMITE_SAQUES, valor):
    if valor > saldo:
        return saldo, contagem_saques, "Fundos insuficientes."
    elif valor > limite:
        return saldo, contagem_saques, "O valor do saque excede o limite."
    elif contagem_saques >= LIMITE_SAQUES:
        return saldo, contagem_saques, "Número máximo de saques excedido."
    elif valor > 0:
        saldo -= valor
        contagem_saques += 1
        extrato = f"\nSaque: R$ {valor:.2f}\n"
        return saldo, contagem_saques, extrato
    else:
        return saldo, contagem_saques, "Valor de saque inválido."

# Função para obter extrato (posicional e por palavras-chave)
def obter_extrato(extrato, *, saldo):
    return f"\n================ EXTRATO =================\n{extrato}\nSaldo: R$ {saldo:.2f}\n==========================================\n"

# Função para operações bancárias
def operacoes_bancarias(conta):
    extrato_atual = conta["extrato"]
    saldo_atual = conta["saldo"]
    limite_atual = conta["limite"]
    contagem_saques_atual = conta["contagem_saques"]

    while True:
        print(f"Menu de operações bancárias para a conta número {conta['numero_conta']} pertencente a {conta['proprietario']['nome']}.")
        opcao = input(banking_menu)

        if opcao == "1":  # Depósito
            valor = float(input("Digite o valor do depósito: "))
            saldo_atual, novo_extrato = deposito(saldo_atual, valor)
            extrato_atual += novo_extrato
            print(f"Depósito de R$ {valor:.2f} realizado com sucesso!")

        elif opcao == "2":  # Saque
            valor = float(input("Digite o valor do saque: "))
            saldo_atual, contagem_saques_atual, novo_extrato = saque(
                saldo=saldo_atual,
                limite=limite_atual,
                contagem_saques=contagem_saques_atual,
                LIMITE_SAQUES=conta["LIMITE_SAQUES"],
                valor=valor,
            )
            extrato_atual += novo_extrato
            print(novo_extrato)

        elif opcao == "3":  # Extrato
            print(obter_extrato(extrato_atual, saldo=saldo_atual))

        elif opcao == "4":  # Alterar Limite
            novo_limite = float(input("Digite o novo limite (máximo 1500): "))
            if novo_limite > 1500:
                print("Limite máximo é 1500.")
            elif novo_limite <= conta["total_sacado"]:
                print("Não é possível definir um limite menor ou igual ao total sacado.")
            else:
                limite_atual = novo_limite
                print(f"Limite alterado para R$ {novo_limite:.2f}")

        elif opcao == "5":  # Voltar ao Menu Principal
            # Atualizar os dados da conta antes de sair
            conta["saldo"] = saldo_atual
            conta["extrato"] = extrato_atual
            conta["limite"] = limite_atual
            conta["contagem_saques"] = contagem_saques_atual
            break

        else:
            print("Opção inválida, por favor tente novamente.")

# Função para selecionar um usuário pelo CPF
def selecionar_usuario_por_cpf(usuarios, cpf):
    return next((u for u in usuarios if u["cpf"] == cpf), None)

# Função para selecionar uma conta para um usuário
def selecionar_conta_por_usuario(usuario, contas):
    contas_do_usuario = [conta for conta in contas if conta["proprietario"]["cpf"] == usuario["cpf"]]

    if len(contas_do_usuario) == 1:
        return contas_do_usuario[0]  # Se houver apenas uma conta, retorna ela

    # Se houver mais de uma conta, peça ao usuário para selecionar
    if len(contas_do_usuario) > 1:
        print("Selecione a conta para operar:")
        for idx, conta in enumerate(contas_do_usuario):
            print(f"[{idx + 1}] Conta número: {conta['numero_conta']}, Agência: {conta['agencia']}")

        opcao = int(input("=> ")) - 1
        
        if opcao >= 0 and opcao < len(contas_do_usuario):
            return contas_do_usuario[opcao]

    return None

# Loop principal do sistema
while True:
    opcao = input(main_menu)

    if opcao == "1":  # Fazer operações bancárias
        cpf = input("Digite o CPF do usuário para identificar: ")
        usuario = selecionar_usuario_por_cpf(usuarios, cpf)
        
        if not usuario:
            print("Usuário com esse CPF não encontrado.")
        else:
            conta = selecionar_conta_por_usuario(usuario, contas)
            if not conta:
                print("Conta não encontrada.")
            else:
                operacoes_bancarias(conta)
                

    elif opcao == "2":  # Registrar novo usuário
        registrar_usuario(usuarios)

    elif opcao == "3":  # Registrar nova conta bancária
        registrar_conta_bancaria(usuarios, contas)

    elif opcao == "4":  # Listar usuários
        listar_usuarios(usuarios)

    elif opcao == "5":  # Listar contas bancárias
        listar_contas(contas)

    elif opcao == "6":  # Sair
        break

    else:
        print("Opção inválida, por favor tente novamente.")

# Mensagem de despedida
print("Obrigado por usar nosso sistema. Até logo!")
