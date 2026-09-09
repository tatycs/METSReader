# METSReader — leitor de `METS.xml`

Ferramenta para ler o **METS de um AIP do Archivematica** e conferir, sem abrir o XML cru,
o que o pacote realmente declara: quais arquivos existem, o que foi feito com cada um,
quem fez, sob que direitos e como o pacote está organizado por dentro.

Roda inteiramente no navegador — o arquivo é lido pelo `FileReader` da própria página e
**nada é enviado para lugar nenhum**.

- Em uso: <https://mr.metadoc.com.br/>
- **[Guia de leitura](guia.html)** — o que aparece em cada aba e como interpretar
  ([versão publicada](https://mr.metadoc.com.br/guia.html))

## Para que serve

O METS de um AIP tem, com facilidade, milhares de linhas: um pacote pequeno, de cinco
documentos, passa de sete mil. Abrir isso num editor de texto para responder a perguntas
simples — *este PDF foi normalizado?*, *qual o hash registrado?*, *que direito está preso a
esta peça?* — é trabalhoso e propenso a erro.

O METSReader resolve as referências que o METS deixa em aberto: liga cada `mets:file` aos
seus `dmdSec` e `amdSec` pelos atributos `DMDID` e `ADMID`, e resolve cada `fptr` do
`structMap` do `FILEID` para o caminho real do arquivo. O que era um emaranhado de
identificadores vira uma leitura por objeto.

## Como usar

**No navegador**, em <https://mr.metadoc.com.br/>: clique em *Selecionar METS.xml* e
escolha o arquivo. Ele fica na sua máquina.

**Localmente**, sem servidor nem dependência — é um arquivo só:

```
abrir index.html no navegador
```

O seletor aceita `.xml` e `.mets`. O arquivo esperado é o `METS.<uuid>.xml` da raiz do AIP
(o mesmo que o Archivematica grava dentro do pacote e no `submissionDocumentation`).

## O que ele mostra

Seis abas, todas construídas a partir do mesmo METS. O
**[guia de leitura](guia.html)** explica cada campo; em resumo:

| Aba | O que traz |
|---|---|
| **Visão geral** | contadores de `mets:file`, objetos, eventos, agentes e direitos PREMIS, e de divisões do `structMap` |
| **Objetos** | um bloco por `mets:file`, com os metadados descritivos (`dmdSec`) e de preservação (`amdSec`) que o arquivo referencia |
| **Eventos** | todos os `premis:event` do pacote |
| **Agentes** | todos os `premis:agent` |
| **Direitos** | cada `premis:rightsStatement` por inteiro |
| **Estrutura** | a árvore de `mets:div` do `structMap`, com os `fptr` resolvidos |

O `objectCharacteristicsExtension` (MIX, JHOVE e o que mais o Archivematica embutir) é
exibido em blocos recolhíveis, preservando os nomes qualificados dos elementos.

## O que ele não faz

- **Não valida** o METS contra o XSD, nem o PREMIS contra o Data Dictionary. Ele mostra o
  que está declarado; não diz se está correto.
- **Não recalcula fixidez.** O `messageDigest` exibido é o que o pacote afirma, não uma
  verificação dos arquivos.
- **Não abre os objetos do pacote** — lê só o METS, que é texto. Os PDFs, TIFFs e demais
  arquivos não são tocados.
- **Não altera nada.** É só leitura.

## Estrutura do repositório

```
index.html   a aplicação inteira: HTML, CSS e JavaScript num arquivo só
guia.html    o guia de leitura, publicado junto
CNAME        subdomínio do GitHub Pages
.nojekyll    impede o Jekyll de processar o diretório
```

## Sobre os METS de exemplo

O `.gitignore` exclui `METS*.xml` de propósito. METS de AIP real costumam trazer nome e
usuário de pessoas identificáveis nos `premis:agent` e nas notas de direitos — não é
material para repositório público. Para testar, use um METS seu.

## Licença

[GNU AGPL v3](LICENSE).
