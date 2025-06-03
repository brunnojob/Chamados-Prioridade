#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Chamado {
    char descricao[100]; // descricao do chamado com um limite de 100 caracte
    int prioridade;      // niveis de prioridade (1 alta, 2 media, 3 baixa)
    struct Chamado *prox; // armazena os dados e faz um proximo chamado
} Chamado;

Chamado *inicio = NULL; // chamado começa nulo

// cria um novo chamado.
Chamado* novoChamado(const char *descricao, int prioridade) {
    Chamado *c = (Chamado*)malloc(sizeof(Chamado));
    strcpy(c->descricao, descricao);
    c->prioridade = prioridade;
    c->prox = NULL;
    return c;
}

// funçao coloca o chamado criado na lista por prioridade 
void inserirChamado(const char *descricao, int prioridade) {
    Chamado *novo = novoChamado(descricao, prioridade);

    if (inicio == NULL || prioridade < inicio->prioridade) {
        novo->prox = inicio;
        inicio = novo;
    } else {
        Chamado *atual = inicio;
        while (atual->prox != NULL && atual->prox->prioridade <= prioridade) {
            atual = atual->prox;
        }
        novo->prox = atual->prox;
        atual->prox = novo;
    }
    printf("chamado adicionado com sucesso!\n");
}

// funçao para remover (conclui um chamado) e retorna o proximo por nivel de prioridade
void atenderChamado() {
    if (inicio == NULL) {
        printf("nenhum chamado na fila.\n");
        return;
    }
    Chamado *atendido = inicio;
    inicio = inicio->prox;
    printf("atendendo chamado: %s (prioridade %d)\n", atendido->descricao, atendido->prioridade);
    free(atendido);
}

// funçao para exibir toda a lista de chamados existentes
void mostrarFila() {
    if (inicio == NULL) {
        printf("fila de chamados vazia.\n");
        return;
    }

    Chamado *atual = inicio;
    printf("\n--- chamados na fila ---\n");
    while (atual != NULL) {
        printf("- %s (prioridade %d)\n", atual->descricao, atual->prioridade);
        atual = atual->prox;
    }
}

// calcula a prioridade baseada na idade e se tem deficiencia
int prioridadeIdadeDeficiencia(int idade, int temDeficiencia) {
    if (temDeficiencia) {
        return 1; // prioridade vai ser alta
    }
    if (idade >= 60) {
        return 1;  // alta prioridade
    } else if (idade >= 40) {
        return 2; // prioridade media
    } else {
        return 3; // prioridade baixa
    }
}

// calcula a prioridade pelo nivel de periculosidade 
int prioridadePericulosidade(int nivel) {
    // 1 (muito perigoso) a 4 (nao perigoso)
    switch (nivel) {
        case 1: return 1; // muito perigoso
        case 2: return 1; // alta prioridade
        case 3: return 2; // media prioridade
        case 4: return 3; // baixa prioridade 
        default: return 3; // padrao baixa
    }
}

// calcula a prioridade final baseado em todas outras prioridades
int calcularPrioridadeFinal(int idade, int temDeficiencia, int nivelPericulosidade) {
    int p1 = prioridadeIdadeDeficiencia(idade, temDeficiencia);
    int p2 = prioridadePericulosidade(nivelPericulosidade);

    return (p1 < p2) ? p1 : p2;
}

int main() {
    int opcao;
    char desc[100];
    int idade, temDeficiencia, nivelPericulosidade;

    do {  // começo do codigo ( menu )
        printf("\n--- sistema de ocorrencias ---\n");
        printf("1. novo chamado\n2. atender chamado\n3. mostrar fila\n0. sair\nescolha: ");
        scanf("%d", &opcao);
        getchar(); // descartar o \n nao utilizado

        switch (opcao) {
            case 1:
                printf("descriçao do chamado: ");
                fgets(desc, 100, stdin);
                desc[strcspn(desc, "\n")] = '\0'; 

                printf("idade do paciente: ");
                scanf("%d", &idade);

                printf("tem alguma deficiencia? (1 = Sim /  0 = nao): ");
                scanf("%d", &temDeficiencia);

                printf("nivel de periculosidade do problema (1 = Muito perigoso, 2 = Perigoso, 3 = Pouco perigoso, 4 = nao perigoso): ");
                scanf("%d", &nivelPericulosidade);
                getchar(); 

                int prioridade = calcularPrioridadeFinal(idade, temDeficiencia, nivelPericulosidade);
                inserirChamado(desc, prioridade);  // funçoes criadas a partir da linha 23 ( calcular as prioridades iniciais e a final )
                break;

            case 2:
                atenderChamado(); // funçao que faz o chamado ser atendido
                break;

            case 3:
                mostrarFila(); // funcao que mostra a fila de chamados listados por prioridade
                break;

            case 0:
                printf("programa encerrado.\n"); // encerra o programa
                break;

            default:
                printf("opcao invalidade!\n"); // caso o usuario escolha um opcao invalida
        }
    } while (opcao != 0); // executa o codigo enquanto a opcao for diferente de 0

    return 0;
}
