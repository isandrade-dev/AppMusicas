# AppMusica

Aplicação de console em C# que modela um pequeno catálogo de áudio, com **bandas, álbuns e músicas** de um lado e **podcasts e episódios** do outro. O projeto foi feito para praticar Programação Orientada a Objetos (classes, propriedades, encapsulamento e composição).

Atualmente o `Program.cs` demonstra o uso da parte de **podcast**: cria episódios com convidados, adiciona-os a um podcast e exibe os detalhes ordenados pela ordem do episódio.

## Tecnologias

- C#
- .NET 6 ou superior (usa top-level statements, `new()` com tipo inferido e implicit usings)
- LINQ (`Sum`, `OrderBy`)

## Estrutura do projeto

```
AppMusica/
├── AppMusica.csproj
├── Program.cs      # Ponto de entrada: monta e exibe o podcast
├── Banda.cs        # Banda com lista de álbuns e discografia
├── Album.cs        # Álbum com lista de músicas e duração total
├── Musica.cs       # Música com artista, duração e disponibilidade
├── PodCast.cs      # Podcast com lista de episódios
└── Episodio.cs     # Episódio com ordem, título, duração e convidados
```

## Classes

| Classe | Responsabilidade |
| --- | --- |
| `Banda` | Guarda o nome e uma lista de álbuns. `AdicionarAlbum` adiciona um álbum e `ExibirDiscografia` mostra cada álbum com sua duração. |
| `Album` | Guarda o nome e uma lista de músicas. `DuracaoTotal` soma a duração das músicas e `ExibirMusicasDoAlbum` lista todas elas. |
| `Musica` | Possui nome, artista (`Banda`), duração e se está disponível no plano. `ExibirFichaTecnica` mostra os dados da música. |
| `Podcast` | Possui nome, host e uma lista de episódios. `TotalEpisodios` conta os episódios e `ExibirDetalhes` os lista ordenados. |
| `Episodio` | Possui ordem, título, duração e lista de convidados. A propriedade `Resumo` monta o texto do episódio. |

## Como executar

Pré-requisito: [.NET SDK](https://dotnet.microsoft.com/download) instalado (versão 6 ou superior).

```bash
# clonar o repositório
git clone <url-do-repositorio>
cd AppMusica

# executar
dotnet run
```

## Exemplo de saída

```
Podcast >|TI para Poucos|< apresentado por [Daniel Portugal]

1. Filosofia de software (93 min) - Fernando Roberto, Gabriel Barbosa
2. Aprendendo a aprender (78 min) - Marcos Felício
3. Consciênciologia (87 min) - Flavio Almeida, Gui Lima, Fernanda Fernandes
4. Técnicas de Facilitação (45 min) - Ana Pereira, Mário Francis


Total de episódios: 4.
```

Note que os episódios foram adicionados fora de ordem no `Program.cs`, mas aparecem organizados pelo número do episódio por causa do `OrderBy(e => e.Ordem)`.

## Exemplo de uso das classes de música

As classes `Banda`, `Album` e `Musica` ainda não são usadas no `Program.cs`, mas podem ser testadas assim:

```csharp
Banda banda = new("Os Exemplos");

Musica musica = new(banda, "Primeira Faixa")
{
    Duracao = 210,
    Disponivel = true
};

Album album = new("Álbum de Estreia");
album.AdicionarMusica(musica);
banda.AdicionarAlbum(album);

musica.ExibirFichaTecnica();
album.ExibirMusicasDoAlbum();
banda.ExibirDiscografia();
```

## Conceitos praticados

- Encapsulamento com listas privadas e métodos públicos de adição
- Propriedades somente leitura e propriedades calculadas (expression-bodied)
- Composição entre classes (Banda → Álbum → Música e Podcast → Episódio)
- Consultas com LINQ
- Interpolação de strings

## Melhorias futuras

- Usar as classes de música no `Program.cs`
- Padronizar a unidade de duração (segundos ou minutos) e exibi-la na saída
- Criar um menu interativo no console
- Adicionar avaliações de músicas e episódios

## Autor

Igor Andrade — [GitHub](https://github.com/isandrade-dev) · [LinkedIn](https://www.linkedin.com/in/%C3%ADgor-andrade-079662368/)
