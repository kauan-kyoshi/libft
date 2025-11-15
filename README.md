# Libft (42)

Uma biblioteca C mínima, base do currículo da 42, com reimplementações de funções da libc e utilitários úteis para futuros projetos. Este repositório compila uma biblioteca estática `libft.a` com as funções implementadas neste projeto.


**Sumário**
- O que é a Libft
- Objetivos do projeto
- Regras e normas (Norm, alocação, permitido/proibido)
- Estrutura do repositório
- Funções implementadas neste repo
- Como compilar e usar
- Exemplo rápido de uso
- Testes e depuração
- Competências desenvolvidas
- Avaliação e dicas

## O que é a Libft
A Libft é a sua “biblioteca padrão” pessoal em C. Você reimplementa funções básicas de manipulação de memória, strings e E/S, e as empacota em uma biblioteca estática (`libft.a`) para reutilizá-la em todos os projetos seguintes da 42.

## Objetivos do projeto
- Entender profundamente ponteiros, arrays e strings em C.
- Controlar alocação dinâmica, ciclo de vida de memória e erros.
- Praticar modularização, organização de headers e construção com Makefile.
- Criar uma base reutilizável para futuros projetos (minishell, so_long, etc.).

## Regras e normas
- Estilo: seguir a Norm (Norminette) da 42.
- Biblioteca: gerar `libft.a` (estática), não binários executáveis.
- Funções permitidas: tipicamente `write`, `malloc`, `free` (verifique o enunciado da sua época). Evite outras funções da libc nas reimplementações.
- Alocação: retorne `NULL` em falhas e evite leaks; documente ownership quando a função transfere/faz free.
- Headers: `libft.h` deve expor apenas o que é público/necessário.

## Estrutura do repositório
- `Makefile`: compila todos os `.c` em objetos e cria `libft.a`.
- `libft.h`: protótipos públicos e includes mínimos (`stdlib.h`, `unistd.h`).
- `*.c`: implementações das funções.

## Funções implementadas (este repositório)
As funções abaixo foram implementadas e fazem parte da build atual:

- Conversão e caracteres:
	- `ft_atoi`, `ft_tolower`, `ft_toupper`
- Classificação de caracteres:
	- `ft_isalnum`, `ft_isalpha`, `ft_isascii`, `ft_isdigit`, `ft_isprint`
- Memória:
	- `ft_bzero`, `ft_calloc`, `ft_memchr`, `ft_memcmp`, `ft_memcpy`, `ft_memmove`, `ft_memset`
- Strings (busca/medição/cópia):
	- `ft_strlen`, `ft_strchr`, `ft_strrchr`, `ft_strncmp`, `ft_strnstr`
	- `ft_strlcpy`, `ft_strlcat`, `ft_strdup`
- Strings (criação/transformação):
	- `ft_substr`, `ft_strjoin`, `ft_strtrim`, `ft_split`, `ft_itoa`
	- `ft_striteri`, `ft_strmapi`
- Saída em fd:
	- `ft_putchar_fd`, `ft_putstr_fd`, `ft_putendl_fd`, `ft_putnbr_fd`


## Como compilar
Requisitos: `cc` (ou `gcc/clang`) e `make`.

```bash
make        # compila e gera libft.a
make clean  # remove .o
make fclean # remove .o e libft.a
make re     # recompila do zero
```

Após `make`, o arquivo `libft.a` estará na raiz do projeto.

## Como usar em outro projeto
Inclua o header e linke a biblioteca estática ao compilar seu programa.

```c
// main.c
#include "libft.h"
#include <unistd.h>

int main(void) {
		const char *s = "hello";
		char *joined = ft_strjoin(NULL, "world"); // ver função deste repo
		ft_putendl_fd((char *)s, 1);
		ft_putendl_fd(joined, 1);
		free(joined);
		return 0;
}
```

```bash
# Exemplo de compilação e link:
cc -Wall -Wextra -Werror -I. -c main.c -o main.o
cc main.o libft.a -o app
./app
```

## Testes e depuração
- Crie pequenos programas `main.c` para testar cada função isoladamente.
- Use `valgrind` para checar leaks e acessos inválidos de memória:
	```bash
	valgrind --leak-check=full ./app
	```
- Se usar a Norm, valide com a Norminette; mantenha funções curtas e coesas.

## Competências desenvolvidas
- Fundamentos de C: ponteiros, arrays, `const`, tipos e conversões.
- Gestão de memória: `malloc/free`, ownership, leaks e double-free.
- Manipulação de strings e buffers binários.
- Organização de projeto: headers, separação de interface/implementação.
- Build systems: Makefile, geração de bibliotecas estáticas.
- Boas práticas: tratamento de erros, contratos de função, testes mínimos.
