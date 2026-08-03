<h1 align="center"><a href="https://github.com/codespearhead/vestibulares-banco-de-questoes">vestibulares-banco-de-questoes</a></h1>

<p align="center">
    <br>
  <a href="https://www.flaticon.com/free-icon/oracle-data-integrator_5805699?term=oracle&page=1&position=13&origin=search&related_id=5805699">
    <img src="https://cdn-icons-png.flaticon.com/512/5805/5805699.png" width="120px" height="120px"/>
  </a>
  <br><br>
Banco de questões de código aberto de vestibulares do ensino médio
  <br>
</p>

<br>

# A.0 - Como visualizar as questões do banco de questões

> [!IMPORTANT]
> O [./index.html](./index.html) também consegue abrir o arquivo `testes.json` referente aos prompts.

A.1 - Abra o arquivo [./index.html](./index.html) no seu navegador web.

A.2 - Clique no botão "Modo de Visualização".

A.3 - Clique em "Selecionar pasta" e selecione a pasta [./banco-de-questoes](./banco-de-questoes/).

A.4 - Filtre as provas desejadas na seção "Séries de provas" e os conteúdos desejados na seção "Conteúdos", e em seguida clique no botão "Abrir questões" presente na seção "Resultado".

# B.0 - Como adicionar uma nova prova ao banco de questões

## B.1.0 - Converter prova de PDF para JSON.

> [!IMPORTANT]
> Todas as provas até então foram mineradas (transformadas em arquivo JSON) exclusivamente com ou o `GPT 5.5` ou o `GPT-5.6 Sol`, ambos com o valor da propriedade "intelligence" da conversa alterada de "Instant" (valor padrão) para "Medium".

B.1.1 - Envie a seguinte mensagem ao LLM junto com o arquivo PDF do caderno de prova, o arquivo PDF do gabarito e o [prompt 01](./prompt/01-minerar-questoes-e-gabarito/prompt.json).

```
Siga as especificações contidas no arquivo `prompt.json`.
```

> [!IMPORTANT]
> Caso o LLM se recuse a gerar a resposta após a `validacaoPrevia`, vide [tratamento_de_recusas_pelo_llm](./prompt/01-minerar-questoes-e-gabarito/tratamento_de_recusas_pelo_llm/).

B.1.2 - Se tudo der certo, será enviado no chat o conteúdo de um arquivo JSON. Salve-o em um arquivo JSON temporário, como `a.json`, e abra tal arquivo no "Modo de Edição" presente ao abrir o [./index.html](./index.html) no seu navegador web. Se as questões extraídas estiverem de acordo com o PDF da prova, envie:

```
Aprovado. Continue.
```

B.1.3 - Trate a saída do LLM conforme a seção abaixo.

## B.2.0 - Tratar saída do LLM usando o "Modo de Edição" do [./index.html](./index.html)

Embora o LLM consiga fazer quase tudo, ele ainda possui limitações, as quais precisam ser tratadas manualmente. Após a geração do arquivo JSON pelo LLM, abra-o no "Modo de edição" do [./index.html](./index.html).

> [!IMPORTANT]
> As alterações no arquivo [./index.html](./index.html) não são refletidas automaticamente no navegador, então caso este arquivo seja alterado, atualize a página do navegador. Após qualquer alteração no arquivo JSON carregado no "Modo de Edição", como a adição de imagem a uma questão, navegue para a questão anterior ou posterior e retorne para a questão atual, pois tal ação força o navegador a ler novamente o arquivo JSON local, o que permite garantir que os dados, por exemplo uma imagem, tenha sido de fato persistido no arquivo JSON em questão.

### B.2.1.0 - `[TODO:ADICIONAR_IMAGEM]`: a questão possui uma imagem.

B.2.1.1 - Converta todo o PDF do caderno de prova para imagens usando [este site](https://www.ilovepdf.com/pt/pdf_para_jpg).

B.2.1.2 - Abra a imagem onde está a questão desejada no Microsoft Paint, selecione apenas a imagem desejada com sua ferramenta de seleção e aperte CRTL+C.

B.2.1.3 - Clique no botão "Colar imagem da área de transferência".

### B.2.2.0 - `[TODO:ADICIONAR_TERMO_DESTACADO]`: a questão possui um termo destacado o qual não é detectável na extração textual, como termos em negrito ou sublinhados.

B.2.2.1 - Adicione manualmente `**` ao redor da frase que deve ser destacada usando do botão "Editar questão" presente na página para ele passe a aparecer sublinhado, e exclua o termo `[TODO:ADICIONAR_TERMO_DESTACADO]`.

### B.2.3.0 - `[TODO:ADICIONAR_FONTE]`: adicione a URL da página que contém o caderno de prova e o gabarito.

B.2.3.1 - Clique no botão "Editar questão", substitua o `[TODO:ADICIONAR_FONTE]` pela URL e clique em "Validar e salvar".

## B.3.0 - Registrar prova no banco de questões

B.3.1 - Adicione o arquivo JSON tratado da prova em [banco-de-questoes](./banco-de-questoes/).

B.3.2 - Envie a seguinte mensagem ao LLM junto com o arquivo JSON tradado da prova, o [indice_tematico_questoes](./banco-de-questoes/indice_tematico_questoes.json) e o [prompt 02](./prompt/02-classificar-conteudo-questoes/prompt.json).

```
Siga as especificações contidas no arquivo `prompt.json`.
```

B.3.3 - Substitua o arquivo [indice_tematico_questoes](./banco-de-questoes/indice_tematico_questoes.json) pelo disponibilizado pelo LLM na etapa anterior.

# C.0 - Como executar a suíte de testes dos [prompts](./prompt/)

C.1 - Forneça ao LLM todo o conteúdo da pasta do prompt.

C.2 - Envie a seguinte mensagem junto ao conteúdo fornecido na etapa anterior:

```
Leia o arquivo [A.1] e execute as instruções definidas em [A.2] apenas para as questões citadas em [A.1].

Para cada questão processada, compare o resultado da extração gerada com o conteúdo da propriedade [B.1] correspondente presente em [A.1].

Ao final, informe quaisquer divergências encontradas, indicando a questão e os campos que diferem.

O objetivo desta conversa é validar se o [A.1] continua produzindo os mesmos resultados após as alterações que fiz nele.

[A.1] `testes.json`
[A.2] `prompt.json`
[B.1] `saida_esperada`
```
