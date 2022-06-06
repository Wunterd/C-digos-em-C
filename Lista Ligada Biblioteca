#include <stdio.h>
#include <stdlib.h>

struct aluno {
	int identificador;
	char nome[30];
};

struct celula {
	struct aluno dados;
	struct celula *proximo;
	struct celula *anterior;
};

struct listaligada {
	struct celula *primeira;
	struct celula *ultima;
	int total_elementos;
};

typedef struct listaligada Tlistaligada;
typedef struct celula Tcelula;
typedef struct aluno Taluno;

Tlistaligada* criar_lista() {

	Tlistaligada *lista;
	lista =(Tlistaligada *) malloc(sizeof(Tlistaligada));

	if (lista == 0) {
		printf("\n Erro: Nao ha memoria suficiente \n");
		exit(1);
	}

	lista->total_elementos = 0;
	lista->primeira = NULL;
	lista->ultima = NULL;

	return lista;

}

void adicionar_no_comeco(Tlistaligada *lista, Taluno aluno_adicionado) {

	Tcelula *nova;
	nova = (Tcelula*)malloc(sizeof(Tcelula));

	if (nova == 0) {
		printf("\n Erro: Nao ha memoria suficiente \n");
		exit(1);
	}

	nova->dados = aluno_adicionado;
	nova->proximo = NULL;
	nova->anterior = NULL;

	//lista esta vazia
	if (lista->total_elementos == 0) {
		lista->primeira = nova;
		lista->ultima = nova;
	} else {
		nova->proximo = lista->primeira;
		lista->primeira->anterior = nova;
		lista->primeira = nova;
	}
	lista->total_elementos++;

}

void adicionar_no_final(Tlistaligada *lista, Taluno aluno_adicionado) {

	if (lista->total_elementos == 0) {
		adicionar_no_comeco(lista, aluno_adicionado);
	} else {

		Tcelula *nova;
		nova = (Tcelula*) malloc(sizeof(Tcelula));

		if (nova == 0) {
			printf("\n Erro: Nao ha memoria suficiente \n");
			exit(1);
		}

		nova->dados = aluno_adicionado;
		nova->proximo = NULL;
		lista->ultima->proximo = nova;
		nova->anterior = lista->ultima;
		lista->ultima = nova;

		lista->total_elementos++;
	}
}

void imprimir_lista(Tlistaligada *lista) {
	if (lista->total_elementos == 0) {
		printf("\n[ ] - lista vazia \n");
	} else {
		Tcelula *atual = lista->primeira;

		printf("[");
		for (int i = 0; i < lista->total_elementos; i++) {
			printf("%d %s;", atual->dados.identificador, atual->dados.nome);
			atual = atual->proximo;
		}
		printf("] \n");
	}
}

void remover_no_inicio(Tlistaligada *lista) {

	if (lista->total_elementos == 0) {
		printf("\n Alerta: A lista esta vazia. \n");
	} else {
		lista->primeira = lista->primeira->proximo;

		if (lista->total_elementos > 1) {
			lista->primeira->anterior = NULL;
		}

		lista->total_elementos--;

		if (lista->total_elementos == 0) {
			lista->ultima = NULL;
		}
	}
}

void remover_no_final(Tlistaligada *lista) {

	if (lista->total_elementos == 0) {
		printf("\n Alerta: A lista esta vazia. \n");
	}

	if (lista->total_elementos == 1) {
		remover_no_inicio(lista);
	} else {
		Tcelula *penultima = lista->ultima->anterior;
		penultima->proximo = NULL;
		lista->ultima = penultima;
		lista->total_elementos--;
	}
}


void buscar_e_imprimir_aluno(Tlistaligada *lista, int identificador) {
	if (lista->total_elementos == 0) {
		printf("\n Alerta: A lista esta vazia. \n");
	} else {
		Tcelula *atual = lista->primeira;

		for (int i = 0; i < lista->total_elementos; i++) {
			if (atual->dados.identificador == identificador) {
				printf("Aluno encontrado: %d %s \n", atual->dados.identificador, atual->dados.nome);
				return;
			}
			atual = atual->proximo;
		}
		printf("\n Aluno nao encontrado. \n");
	}
}


void adicionar_celula_na_posicao(Tlistaligada *lista, Taluno aluno_adicionado, int posicao) {

	if (lista->total_elementos == 0) {
		adicionar_no_comeco(lista, aluno_adicionado);
	} else {
		if (posicao < 0 || posicao > lista->total_elementos) {
			printf("\n Alerta: Posicao invalida. \n");
		} else {
			Tcelula *nova;
			nova = (Tcelula*)malloc(sizeof(Tcelula));

			if (nova == 0) {
				printf("\n Erro: Nao ha memoria suficiente \n");
				exit(1);
			}

			if (posicao == 0) {
				adicionar_no_comeco(lista, aluno_adicionado);
			} else if (posicao == lista->total_elementos) {
				adicionar_no_final(lista, aluno_adicionado);
			} else {
				Tcelula *atual = lista->primeira;
				for (int i = 0; i < posicao - 1; i++) {
					atual = atual->proximo;
				}
				nova->dados = aluno_adicionado;
				nova->proximo = atual->proximo;
				nova->anterior = atual;
				atual->proximo->anterior = nova;
				atual->proximo = nova;
				lista->total_elementos++;
			}
		}
	}
}

void remover_celula_na_posicao(Tlistaligada *lista, int posicao) {

	if (lista->total_elementos == 0) {
		printf("\n Alerta: A lista esta vazia. \n");
	} else {
		if (posicao < 0 || posicao > lista->total_elementos) {
			printf("\n Alerta: Posicao invalida. \n");
		} else {
			if (posicao == 0) {
				remover_no_inicio(lista);
			} else if (posicao == lista->total_elementos) {
				remover_no_final(lista);
			} else {
				Tcelula *atual = lista->primeira;
				for (int i = 0; i < posicao - 1; i++) {
					atual = atual->proximo;
				}
				atual->proximo = atual->proximo->proximo;
				atual->proximo->anterior = atual;
				lista->total_elementos--;
			}
		}
	}
}

void verificar_se_aluno_existe_pelo_nome(Tlistaligada *lista, char *nome) {
	if (lista->total_elementos == 0) {
		printf("\n Alerta: A lista esta vazia. \n");
	} else {
		Tcelula *atual = lista->primeira;

		for (int i = 0; i < lista->total_elementos; i++) {
			if (strcmp(atual->dados.nome, nome) == 0) {
				printf("Aluno encontrado: %d %s \n", atual->dados.identificador, atual->dados.nome);
				return;
			}
			atual = atual->proximo;
		}
		printf("\n Aluno nao encontrado. \n");
	}
}

void liberar_memoria(Tlistaligada *lista) {
	if (lista->total_elementos == 0) {
		printf("\n Alerta: A lista esta vazia. \n");
	} else {
		Tcelula *atual = lista->primeira;
		Tcelula *aux;
		for (int i = 0; i < lista->total_elementos; i++) {
			aux = atual->proximo;
			free(atual);
			atual = aux;
		}
		lista->primeira = NULL;
		lista->ultima = NULL;
		lista->total_elementos = 0;
	}
}
