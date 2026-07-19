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

## A - Como visualizar as questões do banco de questões

> [!IMPORTANT]
> O `index.html` também consegue abrir o arquivo `testes.json` referente aos prompts.

A.01 - Abra o arquivo `index.html` no seu navegador web.

A.02 - Selecione o arquivo desejado da pasta `banco-de-questoes`.

## B - Como executar os prompts

B.01 - Leia a propriedade `entrada` do prompt desejado para saber o que enviar junto a ele.

B.02 - Leia o conteúdo da propriedade `validacaoPrevia`.

B.03 - Envie a seguinte mensagem junto aos arquivos anexados:

```
Siga as especificações contidas no arquivo `prompt.json` para processar a prova.
```

B.04 - Abra o JSON recebido no visualizador de provas (`index.html`) e confirme manualmente que esse arquivo está de acordo como o esperado. Em caso positivo, responda com "Continue", e caso o LLM se recuse por causa de limitações no tamanho do JSON, diga para ler as regras em "processamentoIntegral" novamente.

## C - Como executar os testes

C.01 - Forneça ao LLM todo o conteúdo da pasta do prompt (ex.: `prompt\01-minerar-questoes-e-gabarito`).

C.02 - Envie a seguinte mensagem junto ao conteúdo fornecido na etapa anterior:

```
Leia o arquivo [A.1] e execute as instruções definidas em [A.2] apenas para as questões citadas em [A.1].

Para cada questão processada, compare o resultado da extração gerada com o conteúdo da propriedade [B.1] correspondente presente em [A.1].

Ao final, informe quaisquer divergências encontradas, indicando a questão e os campos que diferem.

O objetivo desta conversa é validar se o [A.1] continua produzindo os mesmos resultados após as alterações que fiz nele.

[A.1] `testes.json`
[A.2] `prompt.json`
[B.1] `saida_esperada`
```

## D - Como tratar saída do LLM

Embora o LLM consiga fazer quase tudo, ele ainda possui limitações, as quais devem ser lidadas manualmente. Após a geração do arquivo JSON pelo LLM, pesquise pelo termo `[TODO:` nele e faça as alterações abaixo de acordo com o que você vê no respectivo arquivo PDF.

> [!IMPORTANT]
> As alterações nos arquivos deste projetos não são refletidas automaticamente no `index.html`, então caso este arquivo seja alterado, atualize a página do navegador. Após qualquer alteração nos arquivos JSON, como a adição de imagem a uma questão, navegue para a questão anterior ou posterior e volte para a questão atual, pois tal ação força o navegador a ler novamente o arquivo JSON local, o que permite garantir que os dados, que nesse caso é uma imagem, foi de fato persistido.

D.01.0 - `[TODO:ADICIONAR_IMAGEM]`: a questão possui uma imagem.

D.01.1 - Converta todo o PDF para imagens usando o seguinte site: https://www.ilovepdf.com/pt/pdf_para_jpg .

D.01.2 - Abra a imagem onde está a questão desejada no Microsoft Paint, selecione apenas a imagem desejada com sua ferramenta de seleção e aperte CRTL+C.

D.01.3 - Clique no botão "Colar imagem da área de transferência".

D.01.4 - Selecione o termo citado no item [D.01.0] no JSON em questão e aperte CRTL+V.

D.02 - `[TODO:ADICIONAR_TERMO_DESTACADO]`: a questão possui um termo destacado o qual não é detectável na extração textual, como termos em negrito ou sublinhados. Adicione manualmente `**` ao redor do termo em questão para que ele fique sublinhado através do botão "Editar questão" presente na página.

D.03 - `[TODO:ADICIONAR_FONTE]`: adicione a URL da página que contém o caderno de prova e o gabarito.
