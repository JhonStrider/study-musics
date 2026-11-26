# Banco de dados do Repertório Mananciais

A aplicação (`index.html`) não tem dados dentro dela: ao abrir, ela lê estes dois arquivos.

| Arquivo | O que guarda |
|---|---|
| `musicas.json` | O banco de músicas: uma entrada por música, com os acordes **em graus** |
| `repertorios.json` | Os repertórios por data: qual música entrou, em que bloco e em que tom |

Para mudar um repertório ou corrigir uma música, edite o JSON e faça o commit. O site atualiza sozinho no GitHub Pages.

## musicas.json

```json
{
  "versao": 1,
  "musicas": {
    "vem-espirito-de-deus": {
      "titulo": "Vem, Espírito de Deus",
      "artista": "Bruna Olly",
      "tom": "E",
      "sustenidos": true,
      "cifraclub": "bruna-olly/vem-espirito-de-deus",
      "roteiro": "Verso → Refrão → …",
      "secoes": [
        { "nome": "Verso", "deixa": "Aqui eu vim…", "graus": "IV V/VII | I ; IV V/VII | VIm7" },
        { "nome": "Interlúdio", "graus": "I IIIm7 | IV9", "repete": "2x" }
      ],
      "apelidos": ["vem espirito de deus"]
    }
  }
}
```

- A chave (`vem-espirito-de-deus`) é o **id** da música. É ele que os repertórios usam.
- `tom` é o tom original da cifra. Em música menor, termina com `m` (ex.: `"Em"`), e o grau `I` é a tônica menor.
- `graus` guarda a harmonia em graus relativos ao `tom`: `I`, `IIm`, `IV7M(9)`, `bVII`, `#IV`, `V/VII` (baixo no VII). ` | ` separa compassos e ` ; ` separa linhas. O app transforma em acordes no tom que for pedido.
- Campos opcionais:
  - `nomeOficial`: quando o nome que o grupo usa é diferente do nome da gravação.
  - `sustenidos`: força a grafia com sustenidos.
  - `tomPelosAcordes`: o tom foi deduzido pelos acordes.
  - `tab: true` numa seção: mostra o link da tab.
  - `aConfirmar` e `obs`: versão ainda não confirmada.
  - `semCifra`: ainda não tem mapa de acordes.
- `apelidos` serve para a busca. Escreva em minúsculas e sem acento.
- Só harmonia, sem letra.

## repertorios.json

```json
{
  "repertorios": [
    {
      "id": "2026-11-25-quarta",
      "sala": "Quarta",
      "data": "2026-11-25",
      "musicas": [
        { "musica": "vem-espirito-de-deus", "tom": "C", "bloco": "Devocional" },
        { "musica": "faz-chover", "tom": "E", "bloco": "Adoração" }
      ]
    }
  ]
}
```

- `sala`: `Quarta`, `Sexta` ou `Geral`.
- `tom`: o tom tocado naquele dia. Sem `tom`, a música fica no tom original.
- A ordem das músicas no arquivo é a ordem no culto.
