# Projeto-de-um-card-pio-
# Este é um exemplo de um cardápio para uma hamburgueria
def exibir_menu_principal(cardapio):
    print("\n cardápio da hamburgueria:")
    opcoes_principais = []
    for i, categoria in enumerate(cardapio.keys()):
        print(f"{i + 1}. {categoria}")
        opcoes_principais.append(categoria)
    print("0. Sair")
    return opcoes_principais

def exibir_itens_categoria(categoria_escolhida, itens):
    print(f"\n Lanches: {categoria_escolhida.upper()}")
    if isinstance(itens, dict):
        for item, preco in itens.items():
            print(f"- {item}: {preco}")
    else:
        print(f"Não há itens detalhados para {categoria_escolhida}")
    input("Voltar")

def iniciar_cardapio_simples(cardapio):
    while True:
        opcoes = exibir_menu_principal(cardapio)
        
        try:
            escolha = int(input("Escolha uma opção: "))
            
            if escolha == 0:
                print("Volte sempre!")
                break
            elif 1 <= escolha <= len(opcoes):
                categoria_selecionada = opcoes[escolha - 1]
                itens_da_categoria = cardapio[categoria_selecionada]
                
                exibir_itens_categoria(categoria_selecionada, itens_da_categoria)
            else:
                print("Opção inválida.")
        except ValueError:
            print("Entrada inválida. Digite um número.")
cardapio_hamburgueria_simples = {
    "Hamburgueres": {
        "X-Burguer": "R$ 30.00",
        "X-Bacon": "R$ 35.00"
    },
    "Bebidas": {
        "Coca-Cola": "R$ 7.00",
    },
}

print("Bem-vindo à nossa Hamburgueria!")
iniciar_cardapio_simples(cardapio_hamburgueria_simples)
