
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#include <strings.h>
#include <windows.h>
/*
Farmácia
-- Login
-- Cadastrar Produto (Nome, Preço, Tarja)
-- Listar produto
-- Comprar itens
-- Controlar Estoque de Remédios
*/
  menu (){
       printf("\n\n---------Menu----------\n");

        printf("\n1)Cadastrar Produto");
        printf("\n2)Listar produto");
        printf("\n3)Comprar itens");
        printf("\n4)Controlar Estoque de Remédios");
        printf("\n9)Fechar programa");

        printf("\n\nDigite a opção escolhida:");

  }


int main(){

    setlocale(LC_ALL,"");

    struct Cadastro
    {
        int quantidadeProduto;
        char nomeProduto[100], tarjaProduto[100], nomeAtendente[100];
        float precoProduto;
    };

    struct Cadastro cadastro_produto[300];

    int i = 1, quantidadeCadastro = 0,linhaPreco = 0, quantidadeItens = 0,parcelasPagamento,removerProduto;
    int op = 1,linha = 0,senha,pagamento,compra = 1,estoque = 1; // switch e whille
    float preco,totalCompra = 0, multiplicacaoValorProduto, divisaValorCompra;
    char  nomeAtendente[100],novoNome[100];

    while (senha != 123456)
    {

        printf("------Login do sistema------\n\n");

        printf("Digite o nome do Funcionário: ");
        fflush(stdin);
        scanf("%[^\n]s",&nomeAtendente);
        printf("Senha: ");
        scanf("%d",&senha);

        system("cls");
        printf("\nSenha incorreta!!\n\n");

    }
        system("cls");

    switch(senha)
    {
        case 123456:

            system("cls");

            while (op != 9)
                {
                menu();

                scanf("%d",&op);

                system("cls");
                printf("\nFuncionário: %s\n\n",nomeAtendente);

                switch (op)
                {

                    case 1:

                        printf("\n-------CADASTRAR PRODUTOS-------");

                        while(op !=0)
                        {
                            printf ("\n\n#Produto %i\n", i);
                            printf ("Nome do Produto: ");
                            fflush(stdin);
                            scanf("%[^\n]s",&cadastro_produto[i].nomeProduto );

                            printf ("Preço: ");
                            scanf  ("%f",&cadastro_produto[i].precoProduto);

                            printf ("Tarja Produto: ");
                            fflush(stdin);
                            scanf("%[^\n]s",&cadastro_produto[i].tarjaProduto);

                            printf ("Quantidade do Produto: ");
                            scanf ("%d",&cadastro_produto[i].quantidadeProduto);


                            printf ("\n\nPRODUTO: %s   PREÇO: R$%.2f   TARJA: %s     QUANTIDADE: %d unidades", cadastro_produto[i].nomeProduto,cadastro_produto[i].precoProduto,cadastro_produto[i].tarjaProduto, cadastro_produto[i].quantidadeProduto);
                            i++;
                            quantidadeCadastro++;

                            printf("\n\nDigite 0 para encerrar o cadastro ou 1 para continuar:");
                            scanf("%d",&op);

                        }
                        system("cls");
                        break;

                    case 2:

                        while(op !=0)
                        {
                            printf("\n-------LISTAR PRODUTODS-------\n");

                            for ( i= 1; i <= quantidadeCadastro; i++)
                            {

                                printf ("\n#Produto %i", i);
                                printf ("\nPRODUTO: %s   PREÇO: R$%.2f   TARJA: %s     QUANTIDADE: %d unidades\n\n", cadastro_produto[i].nomeProduto,cadastro_produto[i].precoProduto,cadastro_produto[i].tarjaProduto, cadastro_produto[i].quantidadeProduto);
                            }

                            printf("\n\nDigite 0 para voltar ao MENU: ");
                            scanf("%d",&op);
                        }

                        system("cls");
                        break;

                    case 3:

                        while(compra != 0)
                        {
                            printf("\n--------PRODUTOS DA LOJA--------");
                            for ( i= 1; i <= quantidadeCadastro; i++)
                            {
                                printf ("\n#Produto %i", i);
                                printf ("\nPRODUTO: %s   PREÇO: R$%.2f   TARJA: %s     QUANTIDADE: %d unidades\n\n", cadastro_produto[i].nomeProduto,cadastro_produto[i].precoProduto,cadastro_produto[i].tarjaProduto, cadastro_produto[i].quantidadeProduto);
                            }


                            printf("\n\n-------COMPRAR ITENS-------");


                            printf("\n\nDigite o numero do produto: ");
                            scanf ("%d", &linha);

                            if ( linha <= quantidadeCadastro )
                            {
                                printf("\nQuantidade do produto: ");
                                scanf ("%d",&quantidadeItens);

                                if (quantidadeItens > cadastro_produto[linha].quantidadeProduto)
                                {
                                    printf("\nQUANTIDADE DO PRODUTO INSUFICIENTE!!\n");
                                }

                                else if (quantidadeItens < cadastro_produto[linha].quantidadeProduto)
                                {
                                    printf("\nTotal: R$ %.2f ", totalCompra);

                                    multiplicacaoValorProduto = cadastro_produto[linha].precoProduto * quantidadeItens; // valor da compra
                                    totalCompra = totalCompra + multiplicacaoValorProduto; // total compra
                                    cadastro_produto[linha].quantidadeProduto = cadastro_produto[linha].quantidadeProduto - quantidadeItens; // Decremento do estoque

                                    printf("\n Valor Produto: R$ %.2f x %d unidades = R$ %.2f ", cadastro_produto[linha].precoProduto, quantidadeItens,multiplicacaoValorProduto );
                                    printf("\nVALOR TOTAL: R$ %.2f ", totalCompra);


                                    while(op !=0)//WHILE OP PAGAMENTO
                                    {
                                        printf("\n\n\n--------FORMAS DE PAGAMENTO--------\n");
                                        printf("\n1)Dinheiro (10%% de desconto)");
                                        printf("\n2)Debito (5%% de desconto) ");
                                        printf("\n3)Credito avista ou parcelado ");


                                        printf("\n\nDigite a opção escolhida: ");
                                        scanf("%d",&pagamento);


                                        switch(pagamento)
                                        {
                                            case 1:
                                                printf("\nVALOR TOTAL: R$ %.2f ", totalCompra * 0.9);
                                                printf ("Pagamento Aprovado!!!");
                                                break;

                                            case 2:
                                                printf("\nVALOR TOTAL: R$ %.2f ", totalCompra * 0.95);
                                                printf ("Pagamento Aprovado!!!");
                                                break;

                                            case 3:
                                                printf("\nVALOR TOTAL: R$ %.2f ", totalCompra);

                                                printf("\n\nDigite a quantidade de parcelas: ");
                                                scanf("%dx",&parcelasPagamento);

                                                divisaValorCompra =  totalCompra / parcelasPagamento;

                                                printf("\nValor Produto: R$ %.2f / %d parcelas = %d x R$%.2f ",totalCompra , parcelasPagamento, parcelasPagamento , divisaValorCompra);

                                                printf ("Pagamento Aprovado!!!");
                                                break;

                                            default:
                                                printf("\nOPIÇÃO INVALIDA!!!!!!");
                                                break;

                                        }
                                        printf("\n\nDIGITE 0 PARA SAIR OU 1 PARA VOLTAR AO PAGAMENTO ");
                                        scanf("%d",&op);
                                        system("cls");

                                    }//WHILE OP PAGAMENTO
                                }//ELSE IF Chechagem de quantidade de produtos

                            }// IF checagem produto
                            else
                            {
                                printf("\n\nPRODUTO NÃO ENCONTRADO!!!\n");
                            }

                            printf("\n\nDIGITE 0 PARA VOLTAR AO MENU OU 1 PARA VOLTAR AS COMPRAS ");
                            scanf("%d",&compra);

                        }//WHILE OP COMPORA

                        system("cls");
                        break;


                    case 4:

                        printf("\n-------CONTROLE DE ESTOQUE-------\n");


                        printf("\n1)ALTERAR NOME");
                        printf("\n2)ALTERAR PREÇO");
                        printf("\n3)ALTERAR TARJA");
                        printf("\n4)ALTERAR QUANTIDADE");

                        printf("\n\nDigite a opção escolhida: ");
                        scanf("%d",&estoque);

                        while(op !=0)
                        {

                            printf("\n\n-------PRODUTODS-------\n");

                            for ( i= 1; i <= quantidadeCadastro; i++)
                            {
                            printf ("\n#Produto %i", i);
                            printf ("\nPRODUTO: %s   PREÇO: R$%.2f   TARJA: %s     QUANTIDADE: %d unidades\n\n", cadastro_produto[i].nomeProduto,cadastro_produto[i].precoProduto,cadastro_produto[i].tarjaProduto, cadastro_produto[i].quantidadeProduto);
                            }
    



                            switch(estoque)
                            {
                                case 1:
                                    printf("\n--------ALTERAR NOME--------");

                                    printf("\nDigite o numero do produto: ");
                                    scanf ("%d", &i);

                                    cadastro_produto[i].nomeProduto;

                                    printf("Novo nome: ");
                                    fflush(stdin);
                                    scanf("%[^\n]s",&cadastro_produto[i].nomeProduto);

                                    printf ("\nPRODUTO: %s  \n\n", cadastro_produto[i].nomeProduto);
                                    break;

                                case 2:
                                    printf("\n--------ALTERAR PREÇO--------");

                                    printf("\nDigite o numero do produto: ");
                                    scanf ("%d", &i);

                                    cadastro_produto[i].precoProduto;

                                    printf("Novo Preço: ");
                                    scanf ("%f",&cadastro_produto[i].precoProduto);

                                    printf ("\nPREÇO: %.2f \n\n", cadastro_produto[i].precoProduto);
                                    break;

                                case 3:
                                    printf("\n--------ALTERAR TARJA--------");

                                    printf("\nDigite o numero do produto: ");
                                    scanf ("%d", &i);
    
                                    cadastro_produto[i].tarjaProduto;

                                    printf("Nova Tarja: ");
                                    fflush(stdin);
                                    scanf("%[^\n]s",&cadastro_produto[i].tarjaProduto);

                                    printf ("\nTARJA: %s  \n\n", cadastro_produto[i].tarjaProduto);
                                    break;
    
                                case 4:
                                    printf("\n--------ALTERAR QUANTIDADE--------");

                                    printf("\nDigite o numero do produto: ");
                                    scanf ("%d", &i);
    
                                    cadastro_produto[i].quantidadeProduto;

                                    printf("\nQuantidade que vai entrar ou sair do estoque : ");
                                    scanf ("%d",&quantidadeItens);

                                    cadastro_produto[i].quantidadeProduto = cadastro_produto[i].quantidadeProduto + (quantidadeItens);

                                    printf ("\nQUANTIDADE: %d  \n\n", cadastro_produto[i].quantidadeProduto);
                                    break;

                                default:
                                    system("cls");
                                    printf("\nOPIÇÃO INVALIDA!!!!!!");
                                    break;

                       }
                        printf("\n\nDIGITE 0 FINALIZAR A ALTERAÇÃO OU 1 PARA CONTINUAR: ");
                        scanf("%d",&op);
                        system("cls");

                    }//While controle de estoque

            default:
            printf("\nOPIÇÃO DE MENU INVALIDA!!!!!!");
            break;

                }//SWITCH MENU
            }//WHILE MENU
    return 0;
    }//SWITCH SENHA
}
