# METSReader — leitor de `METS.xml`

Ferramenta para ler o **METS de um AIP do Archivematica** e conferir, sem abrir o XML
cru, o que o pacote realmente declara. Roda inteiramente no navegador: o arquivo é lido
pelo `FileReader` da própria página — **nada é enviado para lugar nenhum**.

Em uso: <https://mr.metadoc.com.br/>

## O que ele mostra

Seis abas, todas construídas a partir do mesmo METS:

- **Visão geral** — contadores de `mets:file`, de objetos, eventos, agentes e direitos
  PREMIS, e de divisões do `structMap`.
- **Objetos** — um bloco por `mets:file`, com `FILEID`, grupo de uso (`fileGrp/@USE`),
  MIME, tamanho e caminho no pacote; abaixo, os metadados descritivos (`dmdSec`, Dublin
  Core) e os administrativos (`amdSec`) referenciados por `DMDID` e `ADMID`.
- **Eventos** e **Agentes** — visão global de `premis:event` e `premis:agent`.
- **Direitos** — cada `premis:rightsStatement` por inteiro: identificador, `rightsBasis`,
  o bloco da base declarada (copyright, license, statute ou otherRights), cada
  `rightsGranted` com `act`, `restriction`, `termOfGrant`/`termOfRestriction` e notas, e
  os vínculos `linkingObject`/`linkingAgent`. Os direitos também aparecem por arquivo, na
  aba Objetos.
- **Estrutura** — a árvore de `mets:div` do `structMap`, com `LABEL`, `TYPE`, `ORDER`,
  `DMDID` e `ADMID`; cada `fptr` é resolvido do `FILEID` para o caminho do arquivo e o
  grupo de uso, e `mptr` é exibido como ponteiro externo.

O `objectCharacteristicsExtension` (MIX, JHOVE e o que mais o Archivematica embutir) é
exibido em blocos recolhíveis, preservando os nomes qualificados dos elementos.

## Rodar localmente

Não precisa de servidor nem de dependência: é um arquivo só.

```
abrir index.html no navegador
```

O `<input type="file">` aceita `.xml` e `.mets`.

## Publicar no GitHub Pages

Os arquivos ficam na raiz. Settings → Pages → Source: branch `main`, pasta `/`.
O `CNAME` aponta para o subdomínio e o `.nojekyll` evita que o Jekyll processe o
diretório.

## Sobre os METS de exemplo

O `.gitignore` exclui `METS*.xml` de propósito. METS de AIP real costumam trazer nome e
usuário de pessoas identificáveis nos `premis:agent` e nas notas de direitos — não é
material para repositório público. Para testar, use um METS seu.

## Licença

[GNU AGPL v3](LICENSE).
