#include <stdio.h>

#define MAX_CIDADES 100

typedef struct {
    char estado;                // Estado: Uma letra de 'A' a 'H'
    char codigo[5];            // Código da Carta: ex: A01, B03
    char nomeCidade[50];       // Nome da Cidade
    int populacao;             // População
    float area;                // Área em km²
    float pib;                 // PIB
    int pontosTuristicos;      // Número de Pontos Turísticos
} Carta;

void lerCarta(Carta *carta) {
    printf("Digite o estado (A-H): ");
    scanf(" %c", &carta->estado);

    printf("Digite o código da carta (ex: A01): ");
    scanf("%s", carta->codigo);

    printf("Digite o nome da cidade: ");
    scanf(" %[^\n]", carta->nomeCidade); // Lê até a nova linha

    printf("Digite a população: ");
    scanf("%d", &carta->populacao);

    printf("Digite a área (em km²): ");
    scanf("%f", &carta->area);

    printf("Digite o PIB: ");
    scanf("%f", &carta->pib);

    printf("Digite o número de pontos turísticos: ");
    scanf("%d", &carta->pontosTuristicos);
}

float calcularDensidade(Carta c) {
    if (c.area == 0) {
        return 0; // Evitar divisão por zero
    }
    return (float)c.populacao / c.area;
}

void exibirCarta(Carta carta) {
    printf("\n--- Dados da Carta ---\n");
    printf("Estado: %c\n", carta.estado);
    printf("Código da Carta: %s\n", carta.codigo);
    printf("Nome da Cidade: %s\n", carta.nomeCidade);
    printf("População: %d\n", carta.populacao);
    printf("Área: %.2f km²\n", carta.area);
    printf("PIB: %.2f\n", carta.pib);
    printf("Pontos Turísticos: %d\n", carta.pontosTuristicos);
    printf("Densidade Populacional: %.2f habitantes por km²\n", calcularDensidade(carta));
}

// Função para comparar as cartas com base em dois atributos escolhidos
void compararCartas(Carta c1, Carta c2, int atributo1, int atributo2) {
    float valor1_a, valor2_a, valor1_b, valor2_b;
    const char *nome_atributo1, *nome_atributo2;

    // Atributo 1
    switch (atributo1) {
        case 1: // População
            valor1_a = c1.populacao;
            valor2_a = c2.populacao;
            nome_atributo1 = "População";
            break;
        case 2: // Área
            valor1_a = c1.area;
            valor2_a = c2.area;
            nome_atributo1 = "Área";
            break;
        case 3: // PIB
            valor1_a = c1.pib;
            valor2_a = c2.pib;
            nome_atributo1 = "PIB";
            break;
        case 4: // Pontos Turísticos
            valor1_a = c1.pontosTuristicos;
            valor2_a = c2.pontosTuristicos;
            nome_atributo1 = "Pontos Turísticos";
            break;
        case 5: // Densidade Populacional
            valor1_a = calcularDensidade(c1);
            valor2_a = calcularDensidade(c2);
            nome_atributo1 = "Densidade Populacional";
            break;
        default:
            printf("Atributo inválido!\n");
            return;
    }

    // Atributo 2
    switch (atributo2) {
        case 1: // População
            valor1_b = c1.populacao;
            valor2_b = c2.populacao;
            nome_atributo2 = "População";
            break;
        case 2: // Área
            valor1_b = c1.area;
            valor2_b = c2.area;
            nome_atributo2 = "Área";
            break;
        case 3: // PIB
            valor1_b = c1.pib;
            valor2_b = c2.pib;
            nome_atributo2 = "PIB";
            break;
        case 4: // Pontos Turísticos
            valor1_b = c1.pontosTuristicos;
            valor2_b = c2.pontosTuristicos;
            nome_atributo2 = "Pontos Turísticos";
            break;
        case 5: // Densidade Populacional
            valor1_b = calcularDensidade(c1);
            valor2_b = calcularDensidade(c2);
            nome_atributo2 = "Densidade Populacional";
            break;
        default:
            printf("Atributo inválido!\n");
            return;
    }

    // Comparação dos atributos
    printf("\n--- Comparação de cartas ---\n");
    printf("Atributo 1: %s\n", nome_atributo1);
    printf("Carta 1 - %s: %.2f\n", c1.nomeCidade, valor1_a);
    printf("Carta 2 - %s: %.2f\n", c2.nomeCidade, valor2_a);

    if ((atributo1 == 5 && valor1_a < valor2_a) || (atributo1 != 5 && valor1_a > valor2_a)) {
        printf("Resultado: Carta 1 (%s) venceu!\n", c1.nomeCidade);
    } else if ((atributo1 == 5 && valor1_a > valor2_a) || (atributo1 != 5 && valor1_a < valor2_a)) {
        printf("Resultado: Carta 2 (%s) venceu!\n", c2.nomeCidade);
    } else {
        printf("Empate no atributo %s!\n", nome_atributo1);
    }

    printf("\nAtributo 2: %s\n", nome_atributo2);
    printf("Carta 1 - %s: %.2f\n", c1.nomeCidade, valor1_b);
    printf("Carta 2 - %s: %.2f\n", c2.nomeCidade, valor2_b);

    if ((atributo2 == 5 && valor1_b < valor2_b) || (atributo2 != 5 && valor1_b > valor2_b)) {
        printf("Resultado: Carta 1 (%s) venceu!\n", c1.nomeCidade);
    } else if ((atributo2 == 5 && valor1_b > valor2_b) || (atributo2 != 5 && valor1_b < valor2_b)) {
        printf("Resultado: Carta 2 (%s) venceu!\n", c2.nomeCidade);
    } else {
        printf("Empate no atributo %s!\n", nome_atributo2);
    }

    // Soma dos atributos
    float soma1 = valor1_a + valor1_b;
    float soma2 = valor2_a + valor2_b;

    printf("\nSoma dos atributos:\n");
    printf("Carta 1 (%s): %.2f\n", c1.nomeCidade, soma1);
    printf("Carta 2 (%s): %.2f\n", c2.nomeCidade, soma2);

    if (soma1 > soma2) {
        printf("Resultado final: Carta 1 (%s) venceu!\n", c1.nomeCidade);
    } else if (soma1 < soma2) {
        printf("Resultado final: Carta 2 (%s) venceu!\n", c2.nomeCidade);
    } else {
        printf("Empate na soma dos atributos!\n");
    }
}

int main() {
    Carta cartas[2];

    printf("Insira os dados da primeira carta:\n");
    lerCarta(&cartas[0]);

    printf("\nInsira os dados da segunda carta:\n");
    lerCarta(&cartas[1]);

    printf("\n--- Cartas Inseridas ---\n");
    exibirCarta(cartas[0]);
    exibirCarta(cartas[1]);

    int atributo1, atributo2;
    int atributosEscolhidos[5] = {0}; // Para rastrear atributos escolhidos

    // Escolha do primeiro atributo
    do {
        printf("\nEscolha o primeiro atributo para comparação:\n");
        printf("1. População\n");
        printf("2. Área\n");
        printf("3. PIB\n");
        printf("4. Pontos Turísticos\n");
        printf("5. Densidade Populacional\n");
        printf("Digite sua escolha: ");
        scanf("%d", &atributo1);
    } while (atributo1 < 1 || atributo1 > 5);

    atributosEscolhidos[atributo1 - 1] = 1; // Marcar atributo como escolhido

    // Escolha do segundo atributo
    do {
        printf("\nEscolha o segundo atributo para comparação (não pode ser o mesmo):\n");
        for (int i = 1; i <= 5; i++) {
            if (atributosEscolhidos[i - 1] == 0) {
                switch (i) {
                    case 1: printf("1. População\n"); break;
                    case 2: printf("2. Área\n"); break;
                    case 3: printf("3. PIB\n"); break;
                    case 4: printf("4. Pontos Turísticos\n"); break;
                    case 5: printf("5. Densidade Populacional\n"); break;
                }
            }
        }
        printf("Digite sua escolha: ");
        scanf("%d", &atributo2);
    } while (atributo2 < 1 || atributo2 > 5 || atributosEscolhidos[atributo2 - 1] == 1);

    // Chamada da função de comparação
    compararCartas(cartas[0], cartas[1], atributo1, atributo2);

    return 0;
}
    
