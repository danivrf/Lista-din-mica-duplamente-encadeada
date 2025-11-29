# Intituto Federal de Ciencia e Tecnologia de Goiás - IFG

<p align="center">
<a href= "https://www.fiap.com.br/"><img src="logo preta-01.png" alt="FIAP - Faculdade de Informática e Admnistração Paulista" border="0" width=40% height=40%></a>
</p>

<br>

# lista dinâmica duplamente encadeada



## 📜 Descrição

Este projeto implementa uma lista dinâmica duplamente encadeada em linguagem C, utilizando o conceito formal de Tipo Abstrato de Dados (TAD).
O objetivo é demonstrar uma estrutura de dados eficiente para inserção, remoção e busca de elementos, mantendo flexibilidade e operação em tempo dinâmico, sem limites pré-definidos de tamanho.

O programa oferece as seguintes funcionalidades:

Inserir elementos no início da lista

Inserir elementos no fim da lista

Remover elementos do início

Remover elementos do fim

Buscar elemento pelo valor

Buscar elemento pela posição

Destruir toda a lista liberando memória

Essa implementação atende ao que é solicitado nos conteúdos de Estruturas de Dados e Programação Estruturada, permitindo ao estudante praticar:
ponteiros, alocação dinâmica, modularização via TAD, manipulação de registros e listas duplamente encadeadas.

## 🧠 Código-fonte (TAD + Funções + Demonstração no main)

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct no {
    int v;
    struct no *ant;
    struct no *prox;
} No;

typedef struct {
    No *ini;
    No *fim;
    int tam;
} Lista;

void criar(Lista *l) {
    l->ini = NULL;
    l->fim = NULL;
    l->tam = 0;
}

No* novoNo(int x) {
    No *n = (No*) malloc(sizeof(No));
    n->v = x;
    n->ant = NULL;
    n->prox = NULL;
    return n;
}

void insIni(Lista *l, int x) {
    No *n = novoNo(x);
    if (l->ini == NULL) {
        l->ini = n;
        l->fim = n;
    } else {
        n->prox = l->ini;
        l->ini->ant = n;
        l->ini = n;
    }
    l->tam++;
}

void insFim(Lista *l, int x) {
    No *n = novoNo(x);
    if (l->fim == NULL) {
        l->ini = n;
        l->fim = n;
    } else {
        n->ant = l->fim;
        l->fim->prox = n;
        l->fim = n;
    }
    l->tam++;
}

int remIni(Lista *l) {
    if (l->ini == NULL) return 0;
    No *aux = l->ini;
    int x = aux->v;
    if (l->ini == l->fim) {
        l->ini = NULL;
        l->fim = NULL;
    } else {
        l->ini = aux->prox;
        l->ini->ant = NULL;
    }
    free(aux);
    l->tam--;
    return x;
}

int remFim(Lista *l) {
    if (l->fim == NULL) return 0;
    No *aux = l->fim;
    int x = aux->v;
    if (l->ini == l->fim) {
        l->ini = NULL;
        l->fim = NULL;
    } else {
        l->fim = aux->ant;
        l->fim->prox = NULL;
    }
    free(aux);
    l->tam--;
    return x;
}

No* buscaVal(Lista *l, int x) {
    No *p = l->ini;
    while (p != NULL) {
        if (p->v == x) return p;
        p = p->prox;
    }
    return NULL;
}

No* buscaPos(Lista *l, int pos) {
    if (pos < 0 || pos >= l->tam) return NULL;
    No *p = l->ini;
    for (int i = 0; i < pos; i++)
        p = p->prox;
    return p;
}

void destruir(Lista *l) {
    No *p = l->ini;
    while (p != NULL) {
        No *aux = p;
        p = p->prox;
        free(aux);
    }
    l->ini = NULL;
    l->fim = NULL;
    l->tam = 0;
}

void print(Lista *l) {
    No *p = l->ini;
    while (p != NULL) {
        printf("%d ", p->v);
        p = p->prox;
    }
    printf("\n");
}

int main() {
    Lista l;
    criar(&l);

    insIni(&l, 10);
    insIni(&l, 5);
    insFim(&l, 20);
    insFim(&l, 30);

    print(&l);

    printf("rem ini: %d\n", remIni(&l));
    printf("rem fim: %d\n", remFim(&l));
    print(&l);

    No *e1 = buscaVal(&l, 20);
    if (e1) printf("achei valor 20\n");

    No *e2 = buscaPos(&l, 0);
    if (e2) printf("pos 0: %d\n", e2->v);

    destruir(&l);

    return 0;
}
```



## 📋 Licença

<img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><p xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/"><a property="dct:title" rel="cc:attributionURL" href="https://github.com/agodoi/template">MODELO GIT FIAP</a> por <a rel="cc:attributionURL dct:creator" property="cc:attributionName" href="https://fiap.com.br">Fiap</a> está licenciado sobre <a href="http://creativecommons.org/licenses/by/4.0/?ref=chooser-v1" target="_blank" rel="license noopener noreferrer" style="display:inline-block;">Attribution 4.0 International</a>.</p>


