# Engenharia de Requisitos com GenAI - Sistema de Gestão de Eventos (Eventus)

Atividade prática da disciplina: análise do documento de elicitação do sistema da Eventus e produção dos artefatos de especificação, usando IA generativa como apoio.

## Estrutura

```
engenharia-requisitos-genai/
├── README.md
├── analise/
│   ├── requisitos-funcionais.md      (RF01–RF18, com origem e pendências)
│   ├── requisitos-nao-funcionais.md  (RNF01–RNF06 — todos propostos, não validados)
│   ├── regras-de-negocio.md          (RN01–RN09, com as partes pendentes marcadas)
│   └── duvidas-e-lacunas.md          (contradições C1–C2 e perguntas D01–D10 por stakeholder)
└── especificacao/
    ├── historias-de-usuario.md       (13 histórias com critérios de aceitação em Gherkin)
    └── ciclo-de-vida-da-inscricao.md (máquina de estados da inscrição, em Mermaid)
```

## Ferramenta utilizada

Usei o ChatGPT ao longo de toda a atividade, sempre em ciclos curtos: eu pedia uma análise ou um rascunho, comparava com a minha própria leitura do documento e decidia o que aproveitar.

## Como a IA apoiou cada etapa

Na **análise**, o uso mais produtivo foi pedir para a IA cruzar as falas de stakeholders diferentes procurando conflitos. Foi assim que a contradição C1 (comprovante "logo após a inscrição" × inscrição liberada só depois do pagamento) ficou evidente — numa leitura corrida ela passa fácil, porque as duas falas estão em seções diferentes do documento. A classificação inicial em RF/RNF/RN também partiu de um rascunho da IA, que revisei linha a linha.

Na **escolha dos artefatos**, pedi sugestões e recebi a receita esperada: histórias de usuário, critérios BDD, casos de uso para os fluxos complexos, matriz de rastreabilidade e protótipos. Usei essa lista mais como ponto de partida para discutir do que como decisão pronta - o resultado está na seção seguinte.

Na **especificação**, a IA gerou as primeiras versões das histórias e dos cenários Gherkin. O trabalho de revisão foi maior do que eu esperava: a tendência dela é completar lacunas com valores plausíveis, e eu queria exatamente o contrário — que as lacunas ficassem visíveis.

## Por que escolhi estes artefatos

**Histórias de usuário com critérios de aceitação (Gherkin):** a elicitação já veio em formato de desejos em primeira pessoa, por perfil — a conversão para histórias é quase direta e preserva a rastreabilidade até a fala original. Os critérios em Dado/Quando/Então obrigam a decidir o comportamento esperado caso a caso, e foi justamente ao escrevê-los que as ambiguidades apareceram. Adotei uma convenção que considero o ponto central do meu trabalho: cenários que dependem de dúvida aberta ficam marcados como **[BLOQUEADO — Dxx]**, com o esqueleto escrito mas sem valores inventados.

**Máquina de estados da inscrição (Mermaid):** decidi **não** produzir casos de uso textuais, mesmo sendo a recomendação padrão (da IA e, pelo visto, da maioria das abordagens). Meu argumento: a complexidade do Eventus não está nos fluxos de interação — que são curtos e triviais — e sim nas condições que governam a vida de uma inscrição (pode cancelar? reserva vaga? libera para a fila?). Casos de uso espalhariam essas condições por fluxos alternativos de vários documentos; a máquina de estados concentra tudo em um diagrama, onde cada transição referencia a regra (RN) ou a dúvida (D) que a governa. De quebra, o diagrama expôs quais dúvidas são estruturais: D03 e D06 afetam o centro do modelo, então devem ser as primeiras a resolver com os stakeholders.

**O que deixei de fora, de propósito:** protótipos (a elicitação não traz nada sobre interface — qualquer tela seria invenção minha), matriz de rastreabilidade formal (com ~18 RFs, as referências cruzadas por ID entre os arquivos já resolvem; a matriz viraria burocracia) e diagramas UML além da máquina de estados.

## Sugestões da IA: aceitas, modificadas e descartadas

**Aceitas:**

- o cruzamento de falas que revelou C1 e C2;
- a separação entre requisito funcional e regra de negócio em arquivos distintos;
- a sugestão de endereçar cada dúvida a um stakeholder específico, que transformou o arquivo de lacunas num roteiro de segunda entrevista;
- a inclusão de um papel jurídico/DPO na próxima rodada de elicitação (por causa da LGPD em D08).

**Modificadas:**

- os RNFs vieram genéricos ("o sistema deve ser seguro e ter bom desempenho"); reescrevi com métricas concretas e marquei todos como propostas não validadas, já que a elicitação não trouxe nenhum RNF;
- a IA sugeriu que o palestrante visse nome, e-mail e telefone dos inscritos; restringi a proposta a nome e instituição e transformei o resto em pergunta (D08);
- "tempo real" no painel do organizador virou uma meta verificável (10 segundos), sinalizada como número a confirmar.

**Descartadas:**

- casos de uso textuais completos (motivo acima);
- valores inventados para regras não definidas: a IA propôs "cancelamento até 48h antes", "reembolso integral com 7 dias de antecedência" e "reserva de vaga por 15 minutos" com naturalidade, como se estivessem no documento — não estavam. Tudo isso virou dúvida registrada (D01, D02, D06) em vez de regra;
- funcionalidades que nenhum stakeholder pediu: check-in por QR Code, avaliação de eventos pelos participantes e emissão de crachás. Podem até ser boas ideias, mas requisito sem origem na elicitação é escopo inventado.

## O que aprendi sobre o processo

O risco da IA nesta atividade não é errar — é **acertar demais**: ela preenche silenciosamente cada lacuna com uma decisão plausível, e o documento final parece completo sem que ninguém tenha decidido nada. O trabalho de engenharia de requisitos foi menos escrever e mais desfazer suposições: para cada regra que a IA apresentava como certa, perguntar "isso está no documento ou foi inferido?". Quando estava, virou RN; quando não, virou pergunta com dono.
