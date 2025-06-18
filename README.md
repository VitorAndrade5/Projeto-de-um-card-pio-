# Este é um exemplo de um cardápio para uma hamburgueria


Este é um projeto simples tipo aplicação console. Ele simula um um cardápio interativo, pro uma hamburgueria. Em Python que foi desenvolvido, com ele usa uma árvore, dados estruturada. Pra exibir os itens do cardápio.



#cardapio 
class NoCardapio:
    def __init__(self, nome, preco=None):
        self.nome = nome
        self.preco = preco
        self.filhos = []

    def adicionar_filho(self, no_filho):
        
        self.filhos.append(no_filho)

    def __str__(self):
        
        if self.preco:
            return f"{self.nome}: {self.preco}"
        return self.nome

def construir_arvore_cardapio(dados_cardapio):
   
    raiz = NoCardapio("menu")

   
    for categoria_nome, itens_ou_subcategorias in dados_cardapio.items():
        no_categoria = NoCardapio(categoria_nome)
        raiz.adicionar_filho(no_categoria)

      
        if isinstance(itens_ou_subcategorias, dict):
            for item_nome, item_preco in itens_ou_subcategorias.items():
                no_item = NoCardapio(item_nome, item_preco)
                no_categoria.adicionar_filho(no_item)
        else:
            pass 
    return raiz

def exibir_menu_arvore(no_atual):
    
    print(f"{no_atual.nome.upper()}") 
    opcoes_nós = []
    if no_atual.filhos:
        for i, filho in enumerate(no_atual.filhos):
           
            print(f"{i + 1}. {filho.nome} {'- ' + filho.preco if filho.preco else ''}")
            opcoes_nós.append(filho)
    else:
       
        print(f"Não há mais detalhes {no_atual.nome}.")

    
    if no_atual.nome != "Painel de Produtos": 
        print("0. Voltar")
    else:
        print("0. Sair do Painel") 
    return opcoes_nós

def iniciar_cardapio_arvore(cardapio_dados):
  
    raiz_cardapio = construir_arvore_cardapio(cardapio_dados)
    caminho_navegacao = [raiz_cardapio] 

    print("Bem-vindo!") 

    while True:
        no_atual = caminho_navegacao[-1] 

        opcoes_disponiveis = exibir_menu_arvore(no_atual)

        try:
            escolha = int(input("Escolha uma opção:"))

            if escolha == 0:
                if len(caminho_navegacao) > 1:
                    
                    caminho_navegacao.pop()
                else:
                    
                    print("Volte sempre!")
                    break
            elif 1 <= escolha <= len(opcoes_disponiveis):
                
                proximo_no = opcoes_disponiveis[escolha - 1]
                if proximo_no.filhos: 
                    caminho_navegacao.append(proximo_no)
                else:
                    
                    print(f"\nDetalhes do Produto: {proximo_no.nome} - {proximo_no.preco}")
                    input("Pressione Enter para voltar")
            else:
                print("Opção inválida. ")
        except ValueError:
            print("Entrada inválida.")


cardapio_hamburgueria_simples = {
    "Hamburgueres": {
        "X-Burguer": "R$ 30.00",
        "X-Bacon": "R$ 35.00"
    },
    "Bebidas": {
        "Coca-Cola": "R$ 7.00",
    },
    "Acompanhamentos": {
        "Batata Frita P": "R$ 10.00",
        "Batata Frita G": "R$ 15.00"
    }
}

iniciar_cardapio_arvore(cardapio_hamburgueria_simples)
