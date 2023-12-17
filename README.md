// Inclusão de bibliotecas padrão em C
#include <stdio.h>   // Entrada e saída padrão
#include <stdlib.h>  // Funções de alocação de memória, geração de números aleatórios, etc.
#include <time.h>    // Funções relacionadas ao tempo
#include <string.h>  // Funções para manipulação de strings

// Função que troca os valores de duas variáveis
void trocar(int *a, int *b);

// Função que implementa a partição no algoritmo Quicksort
int partition(int array[], int start, int end);

// Função que implementa o algoritmo Quicksort de maneira recursiva
void quickSort(int array[], int start, int end);

// Função para imprimir os elementos de um array
void printArray(int array[], int size);

// Função para gerar um array com números em ordem decrescente
void numeros_decrescentes(int a[], int size);

// Função para gerar um array com números em ordem crescente
void numeros_crescente(int a[], int size);

// Função para gerar um array com números repetidos
void numeros_repetidos(int a[], int size);

// Função para gerar um array com números em ordem aleatória
void numeros_aleatorios(int a[], int size);

int main() {
    // Inicialização do gerador de números aleatórios com a semente baseada no tempo atual
    srand(time(NULL));

    char encerrar[10]; // Uma string para verificar se o usuário deseja encerrar
    int continuar = 1; // Variável de controle para continuar o loop
    int escolha;
    int tamanho = 100;
    int array[100]; // Declaração de um array de inteiros com tamanho 100
    int size = 100;  // Atribuição do tamanho do array

    // Loop principal do programa
    do {
        // Menu de opções para o usuário
        printf("\nEscolha o tipo de lista:\n\n");
        printf("1. Números em Ordem Decrescente\n");
        printf("2. Números em Ordem Crescente\n");
        printf("3. Números com Elementos Repetidos\n");
        printf("4. Números em Ordem Aleatória\n");
        printf("\nEscolha o tipo de lista ou digite 'sair' para encerrar:\n\n");
        scanf("%s", encerrar); // Lê a entrada do usuário

        // Verifica se o usuário deseja encerrar o programa
        if (strcmp(encerrar, "sair") == 0) {
            continuar = 0; // Define continuar como 0 para sair do loop
        } else {
            escolha = atoi(encerrar); // Converte a entrada para um número

            // Verifica se a escolha está dentro dos limites
            if (escolha >= 1 && escolha <= 4) {
                // Switch para lidar com diferentes escolhas do usuário
                switch (escolha) {
                    case 1:
                        printf("Lista em Ordem Decrescente:\n\n");
                        numeros_decrescentes(array, tamanho);
                        break;
                    case 2:
                        printf("Lista em Ordem Crescente:\n\n");
                        numeros_crescente(array, tamanho);
                        break;
                    case 3:
                        printf("Lista com Elementos Repetidos:\n\n");
                        numeros_repetidos(array, tamanho);
                        break;
                    case 4:
                        printf("Lista em Ordem Aleatória:\n\n");
                        numeros_aleatorios(array, tamanho);
                        break;
                    default:
                        printf("Escolha inválida\n");
                }

                // Exibe o array antes da ordenação
                printf("Lista não ordenada:\n\n");
                printArray(array, tamanho);

                // Chama a função de ordenação Quicksort
                quickSort(array, 0, tamanho - 1);

                // Exibe o array após a ordenação
                printf("\nLista ordenada:\n\n");
                printArray(array, tamanho);
            } else {
                printf("Escolha inválida\n");
            }
        }
    } while (continuar);

    // Mensagem de encerramento do programa
    printf("Obrigado pela atenção encerrando programa.........>_<.........\n");
    return 0;
}

// Função que troca os valores de duas variáveis
void trocar(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Função que implementa a partição no algoritmo Quicksort
int partition(int array[], int start, int end) {
    int pivo = array[end];
    int i = (start - 1);

    for (int j = start; j <= end - 1; j++) {
        if (array[j] <= pivo) {
            i++;
            trocar(&array[i], &array[j]);
        }
    }

    // Troca o pivo para a posição correta
    trocar(&array[i + 1], &array[end]);
    return (i + 1);
}

// Função que implementa o algoritmo Quicksort de maneira recursiva
void quickSort(int array[], int start, int end) {
    if (start < end) {
        int pivo = partition(array, start, end);

        // Chamadas recursivas para ordenar as sublistas
        quickSort(array, start, pivo - 1);
        quickSort(array, pivo + 1, end);
    }
}

// Função para imprimir os elementos de um array
void printArray(int array[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");
}

// Função para gerar um array com números em ordem decrescente
void numeros_decrescentes(int a[], int size) {
    for (int i = 0; i < size; i++) {
        a[i] = size - i;
    }
}

// Função para gerar um array com números em ordem crescente
void numeros_crescente(int a[], int size) {
    for (int i = 0; i < size; i++) {
        a[i] = i + 1;
    }
}

// Função para gerar um array com números repetidos
void numeros_repetidos(int a[], int size) {
    for (int i = 0; i < size; i++) {
        a[i] = (i % 10) + 1;
    }
}

// Função para gerar um array com números em ordem aleatória
void numeros_aleatorios(int a[], int size) {
    for (int i = 0; i < size; i++) {
        a[i] = rand() % 100; // Gere números aleatórios
    }
}
