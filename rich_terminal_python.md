# Python `rich`: Terminal Bonito & Produtivo

**Laboratório de Programação — Ciência da Computação • UFPI**

A biblioteca `rich` permite criar saídas de terminal mais bonitas, legíveis e produtivas em Python, com suporte a estilos, cores, tabelas, painéis, árvores, barras de progresso, renderização de Markdown, realce de sintaxe, tracebacks aprimorados, prompts interativos e muito mais.

---

## 1. O que é o `rich`?

O `rich` é uma biblioteca Python usada para **renderizar texto com estilo no terminal**. Com ela, é possível exibir mensagens coloridas, texto em negrito, emojis, tabelas formatadas, painéis, barras de progresso e outros componentes visuais diretamente no console.

Entre seus principais componentes estão:

- `Console`
- `Table`
- `Panel`
- `Tree`
- `Progress`
- `Live`
- `Markdown`
- `Syntax`
- `Status`
- `Columns`
- `Traceback`
- `Prompt`

A biblioteca funciona em **Windows, macOS e Linux**.

### Instalação

```bash
pip install rich
```

---

## 2. Console e estilos básicos

O componente central da biblioteca é o `Console`. Ele substitui ou complementa o uso tradicional de `print()` para exibir mensagens com estilos visuais.

```python
from rich.console import Console

console = Console()

console.print("[bold magenta]Olá[/] [green]mundo[/]! :snake:")
console.print("Erros em [bold red]vermelho[/], avisos em [yellow]amarelo[/].")
```

### Markup e emojis

O `rich` permite usar marcações semelhantes a tags para aplicar estilos no texto.

Exemplos de tags:

- `[bold]`: texto em negrito;
- `[italic]`: texto em itálico;
- `[red]`, `[green]`, `[yellow]`, `[blue]`: cores;
- `[/]`: finaliza o estilo atual.

Também é possível usar emojis no terminal:

```python
console.print("Python é divertido! :snake: :rocket:")
```

Caso você deseje desabilitar o suporte a markup, pode criar o console assim:

```python
console = Console(markup=False)
```

---

## 3. Pretty print e inspeção de objetos

O `rich` também melhora a visualização de estruturas de dados Python, como listas, dicionários e objetos.

```python
from rich import pretty, inspect

pretty.install()  # ativa formatação bonita do print()

dados = {
    "curso": "Lab CC",
    "alunos": ["Ana", "João"],
    "ativo": True
}

print(dados)      # agora colorido e indentado
inspect(dados, methods=True)
```

O recurso `pretty.install()` melhora a saída padrão de objetos complexos. Já a função `inspect()` permite visualizar atributos, métodos e informações internas de objetos.

---

## 4. Regras e alinhamento de texto

O `rich` permite criar divisórias visuais e alinhar textos no terminal.

```python
from rich.console import Console
from rich.rule import Rule
from rich.align import Align

console = Console()

console.print(Rule("[bold blue]Seção 1"))
console.print(Align("Centralizado", align="center"))
```

Esse recurso é útil para organizar seções em aplicações de linha de comando.

---

## 5. Panel: caixas com borda

O componente `Panel` permite exibir mensagens dentro de uma caixa com borda.

```python
from rich.console import Console
from rich.panel import Panel

console = Console()

console.print(Panel.fit(
    "[bold green]Sucesso![/]\nOperação concluída.",
    title="Status",
    border_style="green"
))
```

Esse componente pode ser usado para destacar mensagens importantes, como avisos, erros, confirmações ou resultados de uma operação.

---

## 6. Table: tabelas formatadas

O componente `Table` permite criar tabelas organizadas e visualmente agradáveis no terminal.

```python
from rich.console import Console
from rich.table import Table

table = Table(title="Alunos")
table.add_column("Nome", style="cyan", no_wrap=True)
table.add_column("Média", justify="right")
table.add_row("Ana", "9.2")
table.add_row("João", "8.7")

Console().print(table)
```

Tabelas são úteis para exibir relatórios, resultados de processamento, listas de usuários, métricas, arquivos ou qualquer informação estruturada.

---

## 7. Tree: representação de árvores

O componente `Tree` permite representar estruturas hierárquicas, como diretórios, menus ou dependências.

```python
from rich.console import Console
from rich.tree import Tree

raiz = Tree("Projeto")
src = raiz.add("[bold]src[/]")
src.add("main.py")
src.add("utils.py")
raiz.add("README.md")

Console().print(raiz)
```

Esse recurso é especialmente útil para representar estruturas de projetos de software.

---

## 8. Columns: múltiplas colunas

O componente `Columns` permite distribuir itens em várias colunas no terminal.

```python
from rich.console import Console
from rich.columns import Columns

itens = [f"[cyan]Item {i}[/]" for i in range(1, 7)]
Console().print(Columns(itens, equal=True, expand=True))
```

Esse recurso pode ser usado para exibir listas de opções, comandos disponíveis ou grupos de informações compactas.

---

## 9. Progress: barras de progresso

O `rich` oferece barras de progresso para acompanhar tarefas em execução.

```python
import time
from rich.progress import Progress

with Progress() as progress:
    tarefa = progress.add_task("[green]Baixando...", total=100)
    while not progress.finished:
        progress.update(tarefa, advance=5)
        time.sleep(0.05)
```

Barras de progresso são úteis para tarefas como:

- downloads;
- processamento de arquivos;
- treinamento de modelos;
- análise de dados;
- execução de pipelines.

---

## 10. Status e spinners

O `Console` também oferece suporte a mensagens de status com animações, conhecidas como spinners.

```python
import time
from rich.console import Console

console = Console()

with console.status("[bold blue]Processando..."):
    time.sleep(2)  # seu trabalho aqui

console.print("[green]Pronto![/]")
```

Esse recurso é útil para indicar que uma operação está em andamento, mesmo quando não há uma porcentagem clara de progresso.

---

## 11. Live: painéis atualizados em tempo real

O componente `Live` permite atualizar informações dinamicamente no terminal.

```python
import time
from rich.live import Live
from rich.table import Table

def tabela(tick):
    tb = Table(title=f"Tick {tick}")
    tb.add_column("Item")
    tb.add_column("Valor", justify="right")
    for i in range(3):
        tb.add_row(f"X{i}", str(tick * (i + 1)))
    return tb

with Live(tabela(0), refresh_per_second=4) as live:
    for n in range(1, 6):
        time.sleep(0.5)
        live.update(tabela(n))
```

Esse recurso é útil para criar dashboards de linha de comando, monitores de execução, ferramentas de scraping e visualizações em tempo real.

---

## 12. Syntax: realce de código

O componente `Syntax` permite exibir código com realce de sintaxe.

```python
from rich.console import Console
from rich.syntax import Syntax

code = "def soma(a, b):\n    return a + b\n"
syntax = Syntax(code, "python", theme="monokai", line_numbers=True)
Console().print(syntax)
```

Esse recurso é útil para ferramentas educacionais, CLIs de desenvolvimento, depuradores e geradores de documentação.

---

## 13. Markdown no terminal

O `rich` também consegue renderizar conteúdo Markdown diretamente no terminal.

```python
from rich.console import Console
from rich.markdown import Markdown

md = Markdown("# Título\n*Itálico* **Negrito**\n- Lista 1\n- Lista 2")
Console().print(md)
```

Com isso, é possível exibir documentação, instruções, ajuda de comandos e relatórios em Markdown no terminal.

---

## 14. Tracebacks aprimorados

O `rich` melhora a visualização de erros e exceções em Python.

```python
from rich.traceback import install

install(show_locals=True)  # melhora tracebacks globais

def falha():
    x = 1 / 0

falha()
```

Com `show_locals=True`, o traceback mostra também variáveis locais, o que pode ajudar bastante durante a depuração.

---

## 15. Logging com Rich

O `rich` pode ser integrado ao módulo `logging` do Python para gerar logs mais legíveis.

```python
import logging
from rich.logging import RichHandler

logging.basicConfig(
    level="INFO",
    format="%(message)s",
    handlers=[RichHandler(rich_tracebacks=True)]
)

log = logging.getLogger("app")
log.info("Servidor iniciado")
```

Esse recurso é útil para aplicações CLI, servidores, scripts de automação e ferramentas de desenvolvimento.

---

## 16. Prompt simples

A biblioteca também oferece componentes para entrada de dados pelo usuário.

```python
from rich.prompt import Prompt, Confirm

nome = Prompt.ask("Seu nome", default="Aluno")
ok = Confirm.ask("Deseja continuar?", default=True)

print(nome, ok)
```

O `Prompt.ask()` permite solicitar valores textuais, enquanto `Confirm.ask()` permite perguntas de confirmação.

---

## 17. Progress avançado com múltiplas tarefas

O `Progress` pode ser customizado com colunas, barras e múltiplas tarefas simultâneas.

```python
import time
from rich.progress import Progress, SpinnerColumn, BarColumn, TextColumn

with Progress(
    SpinnerColumn(),
    TextColumn("[progress.description]{task.description}"),
    BarColumn(),
    TextColumn("{task.percentage:>3.0f}%"),
) as progress:
    t1 = progress.add_task("Tarefa A", total=60)
    t2 = progress.add_task("Tarefa B", total=90)
    while not progress.finished:
        progress.update(t1, advance=2)
        progress.update(t2, advance=3)
        time.sleep(0.05)
```

Esse formato é indicado quando o programa executa várias tarefas ao mesmo tempo ou precisa mostrar diferentes etapas de um pipeline.

---

## 18. Boas práticas e dicas

Algumas boas práticas ao usar `rich` em aplicações Python:

- Centralize a saída usando um único objeto `Console()` compartilhado.
- Evite misturar `print()` e `console.print()` em CLIs complexas.
- Use `Panel` e `Table` para estruturar informações importantes.
- Combine `Live` e `Progress` para criar dashboards de terminal.
- Habilite tracebacks ricos durante o desenvolvimento.
- Use `Logging` com `RichHandler` para melhorar a leitura dos logs.
- Prefira componentes visuais quando eles ajudarem na clareza, e não apenas pela estética.

---

## 19. Cheat sheet

```python
from rich.console import Console
from rich.table import Table
from rich.panel import Panel
from rich.progress import Progress
from rich.syntax import Syntax

console = Console()
console.print("[bold green]OK[/]")

tb = Table()
tb.add_column("A")
tb.add_row("1")
console.print(tb)

console.print(Panel("Mensagem", title="Info"))

with Progress() as p:
    t = p.add_task("Baixando", total=100)
    p.update(t, advance=100)

console.print(Syntax("print('hi')", "python"))
```

---

## 20. Conclusões

A biblioteca `rich` eleva a experiência de uso de aplicações de linha de comando em Python. Ela melhora a legibilidade, oferece feedback visual para o usuário e permite criar interfaces de terminal mais agradáveis e produtivas.

Em resumo:

- `rich` melhora a experiência de CLIs;
- facilita a criação de saídas coloridas e organizadas;
- oferece componentes prontos para tabelas, painéis, árvores e progresso;
- integra-se com `logging`, tracebacks e prompts;
- é útil tanto em projetos educacionais quanto em aplicações profissionais.

---

## Referência rápida dos principais componentes

| Componente | Finalidade |
|---|---|
| `Console` | Impressão estilizada no terminal |
| `Table` | Criação de tabelas formatadas |
| `Panel` | Caixas com borda para destaque visual |
| `Tree` | Representação de estruturas hierárquicas |
| `Columns` | Organização de conteúdo em colunas |
| `Progress` | Barras de progresso |
| `Live` | Atualização dinâmica de conteúdo |
| `Syntax` | Realce de código-fonte |
| `Markdown` | Renderização de Markdown no terminal |
| `Traceback` | Tracebacks mais legíveis |
| `RichHandler` | Logs formatados com `logging` |
| `Prompt` e `Confirm` | Entrada interativa de dados |

