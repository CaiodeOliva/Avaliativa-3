#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    int codigo;
    char descricao[50];
    int quantidade;
    float valor;
} Produto;

typedef struct No {
    Produto produto;
    struct No *prox;
} No;

No *inicializaLista() {
    return NULL;
}

No *adicionaProduto(No *lista) {
    Produto novoProduto;
    printf("Digite o codigo do produto: ");
    scanf("%d", &novoProduto.codigo);

    No *aux = lista;
    while (aux != NULL) {
        if (aux->produto.codigo == novoProduto.codigo) {
            printf("Produto com codigo %d ja cadastrado.\n", novoProduto.codigo);
            return lista;
        }
        aux = aux->prox;
    }

    printf("Digite a descricao do produto: ");
    getchar();
    fgets(novoProduto.descricao, sizeof(novoProduto.descricao), stdin);
    novoProduto.descricao[strcspn(novoProduto.descricao, "\n")] = '\0';

    printf("Digite a quantidade do produto: ");
    scanf("%d", &novoProduto.quantidade);

    printf("Digite o valor do produto: ");
    scanf("%f", &novoProduto.valor);

    No *novoNo = (No *)malloc(sizeof(No));
    novoNo->produto = novoProduto;
    novoNo->prox = lista;

    printf("Produto cadastrado com sucesso!\n");

    return novoNo;
}

void imprimeRelatorio(No *lista) {
    printf("\nRelatorio de Produtos:\n");
    No *aux = lista;

    while (aux != NULL) {
        printf("Codigo: %d\n", aux->produto.codigo);
        printf("Descricao: %s\n", aux->produto.descricao);
        printf("Quantidade: %d\n", aux->produto.quantidade);
        printf("Valor: %.2f\n", aux->produto.valor);
        printf("---------------\n");

        aux = aux->prox;
    }
}

No *pesquisaProduto(No *lista, int codigo) {
    No *aux = lista;

    while (aux != NULL) {
        if (aux->produto.codigo == codigo) {
            return aux;
        }
        aux = aux->prox;
    }

    return NULL;
}

No *removeProduto(No *lista, int codigo) {
    No *atual = lista;
    No *anterior = NULL;

    while (atual != NULL && atual->produto.codigo != codigo) {
        anterior = atual;
        atual = atual->prox;
    }

    if (atual != NULL) {
        if (anterior == NULL) {
            lista = atual->prox;
        } else {
            anterior->prox = atual->prox;
        }

        free(atual);
        printf("Produto removido com sucesso!\n");
    } else {
        printf("Produto nao cadastrado.\n");
    }

    return lista;
}

void limpaLista(No *lista) {
    No *aux = lista;
    while (aux != NULL) {
        No *temp = aux;
        aux = aux->prox;
        free(temp);
    }
}

int main() {
    No *lista = inicializaLista();
    int escolha, codigo;
    Produto encontrado;

    do {
        printf("\nMenu:\n");
        printf("1. Adicionar Produto\n");
        printf("2. Imprimir Relatorio\n");
        printf("3. Pesquisar Produto\n");
        printf("4. Remover Produto\n");
        printf("0. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &escolha);

        switch (escolha) {
            case 1:
                lista = adicionaProduto(lista);
                break;
            case 2:
                imprimeRelatorio(lista);
                break;
            case 3:
                printf("Digite o codigo do produto: ");
                scanf("%d", &codigo);
                encontrado = pesquisaProduto(lista, codigo)->produto;
                if (encontrado.codigo != 0) {
                    printf("Produto Encontrado:\n");
                    printf("Codigo: %d\n", encontrado.codigo);
                    printf("Descricao: %s\n", encontrado.descricao);
                    printf("Quantidade: %d\n", encontrado.quantidade);
                    printf("Valor: %.2f\n", encontrado.valor);
                } else {
                    printf("Produto nao encontrado.\n");
                }
                break;
            case 4:
                printf("Digite o codigo do produto a ser removido: ");
                scanf("%d", &codigo);
                lista = removeProduto(lista, codigo);
                break;
            case 0:
                break;
            default:
                printf("Opcao invalida.\n");
        }
    } while (escolha != 0);

    limpaLista(lista);

    return 0;
}