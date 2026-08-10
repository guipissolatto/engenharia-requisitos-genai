# Histórias de Usuário com Critérios de Aceitação

Optei por manter os critérios de aceitação junto de cada história, em vez de um arquivo separado — na prática é assim que o time consome (a história sem os critérios não é implementável, e os critérios soltos perdem o contexto).

Uma convenção importante: quando um comportamento depende de uma dúvida ainda aberta (arquivo `analise/duvidas-e-lacunas.md`), o cenário aparece marcado como **[BLOQUEADO — Dxx]** com o esqueleto escrito, mas sem valores inventados. Preferi deixar o buraco visível a preenchê-lo com uma suposição que pareceria decidida.

---

## Participante

### HU01 — Visualizar catálogo de eventos

**Como** participante, **quero** ver todos os eventos disponíveis em um único lugar, **para** decidir em quais me inscrever sem depender de links avulsos.

```gherkin
Cenário: Listar eventos com inscrições abertas
  Dado que existem eventos publicados com inscrições abertas
  Quando acesso o catálogo de eventos
  Então vejo cada evento com nome, data, horário, local, valor (ou "gratuito") e situação das vagas

Cenário: Evento lotado continua visível
  Dado que um evento atingiu o limite de vagas
  Quando acesso o catálogo
  Então o evento aparece marcado como "lotado" com opção de entrar na lista de espera
```

### HU02 — Inscrever-se em evento gratuito

**Como** participante, **quero** me inscrever em um evento gratuito, **para** garantir minha vaga.

```gherkin
Cenário: Inscrição com vaga disponível
  Dado que o evento é gratuito e tem vagas disponíveis
  Quando confirmo minha inscrição
  Então minha inscrição fica com status "Confirmada"
  E recebo um comprovante de inscrição
  E o número de vagas disponíveis diminui em 1

Cenário: Tentativa de inscrição duplicada
  Dado que já tenho inscrição ativa neste evento
  Quando tento me inscrever novamente
  Então o sistema recusa e me mostra a inscrição existente
```

### HU03 — Inscrever-se em evento pago

**Como** participante, **quero** me inscrever em um evento pago e efetuar o pagamento, **para** ter minha participação confirmada.

```gherkin
Cenário: Inscrição pendente até a confirmação do pagamento (RN05)
  Dado que o evento é pago e tem vagas disponíveis
  Quando concluo a solicitação de inscrição
  Então minha inscrição fica com status "Pendente de pagamento"
  E recebo um comprovante de solicitação (não de confirmação) — ver C1

Cenário: Pagamento confirmado
  Dado que minha inscrição está "Pendente de pagamento"
  Quando a equipe financeira confirma o pagamento
  Então minha inscrição muda para "Confirmada"
  E recebo o comprovante de confirmação

Cenário: [BLOQUEADO — D06] Reserva da vaga durante o pagamento
  Dado que o evento pago tem 1 vaga disponível
  Quando inicio o pagamento
  Então <a vaga é reservada por N minutos | a vaga segue disponível até a confirmação>
  # Não especificado: depende da definição de D06 com a equipe financeira
```

### HU04 — Cancelar a própria inscrição

**Como** participante, **quero** cancelar minha inscrição sem falar com a organização, **para** liberar a vaga quando não puder ir.

```gherkin
Cenário: Cancelamento em evento que permite (RN03)
  Dado que estou inscrito em um evento que permite cancelamento
  E o prazo de cancelamento ainda não expirou
  Quando cancelo minha inscrição
  Então a inscrição muda para "Cancelada"
  E a vaga é liberada (para a lista de espera, se houver)
  E recebo a confirmação do cancelamento

Cenário: Evento que não permite cancelamento (RN03)
  Dado que estou inscrito em um evento que não permite cancelamento
  Quando tento cancelar
  Então o sistema recusa e informa a política do evento

Cenário: [BLOQUEADO — D01] Cancelamento fora do prazo
  Dado que estou inscrito em um evento que permite cancelamento
  E <o prazo limite — não definido> já passou
  Quando tento cancelar
  Então <comportamento a definir com os organizadores>
```

### HU05 — Solicitar reembolso

**Como** participante, **quero** saber se tenho direito a reembolso ao cancelar um evento pago, **para** decidir com clareza.

```gherkin
Cenário: [BLOQUEADO — D02] Cancelamento com direito a reembolso
  Dado que cancelo minha inscrição em um evento pago
  E <as condições de reembolso — não definidas> são atendidas
  Então uma solicitação de reembolso é registrada para a equipe financeira
  # Percentuais e prazos não foram definidos na elicitação; não inventei valores

Cenário: Cancelamento sem direito a reembolso
  Dado que cancelo minha inscrição em um evento pago sem direito a reembolso
  Quando confirmo o cancelamento
  Então o sistema me informa, antes da confirmação, que não haverá reembolso
```

### HU06 — Emitir certificado

**Como** participante, **quero** emitir meu certificado depois do evento, **para** comprovar minha participação.

```gherkin
Cenário: Certificado disponível após o evento (RN07)
  Dado que participei de um evento já realizado
  E atendo à condição de emissão <automática ou presença — BLOQUEADO, D04>
  Quando solicito meu certificado
  Então o sistema gera o certificado com meu nome, o evento e a carga horária

Cenário: Tentativa antes do fim do evento
  Dado que o evento ainda não terminou
  Quando tento emitir o certificado
  Então o sistema recusa e informa a partir de quando estará disponível
```

### HU07 — Inscrever-se em vários workshops do mesmo dia

**Como** participante, **quero** me inscrever em vários workshops que acontecem no mesmo dia, **para** aproveitar melhor o evento.

```gherkin
Cenário: Workshops em horários distintos
  Dado que dois workshops do mesmo dia têm horários que não se sobrepõem
  Quando me inscrevo nos dois
  Então as duas inscrições são aceitas

Cenário: [BLOQUEADO — D07] Workshops com horários sobrepostos
  Dado que dois workshops têm horários sobrepostos
  Quando tento me inscrever no segundo
  Então <bloqueia | alerta e permite | permite — a definir>
  # RN08 é inferida; o comportamento precisa ser confirmado com os organizadores
```

### HU08 — Entrar na lista de espera

**Como** participante, **quero** entrar na lista de espera de um evento lotado, **para** ter chance de participar se abrir vaga.

```gherkin
Cenário: Entrada na lista de espera (RN02)
  Dado que o evento está lotado
  Quando solicito inscrição
  Então entro na lista de espera e sou informado da minha posição

Cenário: [BLOQUEADO — D03] Vaga liberada
  Dado que estou em primeiro na lista de espera
  Quando uma vaga é liberada
  Então <sou inscrito automaticamente | recebo convite com prazo — a definir>
```

---

## Organizador

### HU09 — Criar e configurar evento

**Como** organizador, **quero** cadastrar um evento definindo vagas, valor e política de cancelamento, **para** que o sistema controle as inscrições segundo as regras daquele evento.

```gherkin
Cenário: Cadastro completo
  Dado que informo nome, data, horário, local, limite de vagas, valor (ou gratuito) e política de cancelamento
  Quando publico o evento
  Então ele aparece no catálogo e passa a aceitar inscrições

Cenário: Política de cancelamento é obrigatória (RN03)
  Dado que estou cadastrando um evento
  Quando tento publicar sem definir se o cancelamento é permitido
  Então o sistema exige a definição antes de publicar
```

### HU10 — Acompanhar inscrições em tempo real

**Como** organizador, **quero** acompanhar a quantidade de inscritos dos meus eventos, **para** tomar decisões durante o período de inscrição.

```gherkin
Cenário: Painel de inscrições
  Dado que meu evento está com inscrições abertas
  Quando acesso o painel do evento
  Então vejo confirmadas, pendentes de pagamento, lista de espera e vagas restantes
  E os números refletem novas inscrições em até 10 segundos (RNF02 — meta proposta, a validar)
```

### HU11 — Controle automático de vagas

**Como** organizador, **quero** que o sistema impeça inscrições confirmadas além do limite, **para** não ter que controlar vagas manualmente como era nas planilhas.

```gherkin
Cenário: Última vaga (RN01)
  Dado que o evento tem 1 vaga disponível
  Quando uma inscrição é confirmada
  Então o evento passa a "lotado" e novas solicitações vão para a lista de espera

Cenário: Duas solicitações simultâneas para a última vaga (RNF03)
  Dado que o evento tem 1 vaga disponível
  Quando dois participantes confirmam a inscrição ao mesmo tempo
  Então exatamente um é confirmado e o outro é direcionado à lista de espera
  # Em evento pago, o resultado depende de D06 (reserva de vaga)
```

---

## Equipe financeira

### HU12 — Confirmar pagamentos

**Como** membro da equipe financeira, **quero** confirmar os pagamentos recebidos, **para** liberar as inscrições correspondentes (RN05).

```gherkin
Cenário: Confirmação libera a inscrição
  Dado que existe uma inscrição "Pendente de pagamento" com pagamento identificado
  Quando confirmo o pagamento
  Então a inscrição muda para "Confirmada" e o participante é notificado

Cenário: Pagamento não confirmado
  Dado que uma inscrição está "Pendente de pagamento"
  Quando o pagamento não é confirmado <dentro do prazo — BLOQUEADO, D06>
  Então <a inscrição expira e a vaga é liberada — a definir>
```

---

## Palestrante

### HU13 — Consultar participantes das minhas atividades

**Como** palestrante, **quero** ver a lista de inscritos nas minhas atividades, **para** me preparar para o público.

```gherkin
Cenário: Lista restrita às próprias atividades (RN09)
  Dado que sou palestrante de uma atividade
  Quando consulto a lista de inscritos
  Então vejo apenas os inscritos das minhas atividades
  E apenas os campos autorizados <nome e instituição — proposta, BLOQUEADO por D08>

Cenário: Tentativa de acesso a outra atividade
  Dado que sou palestrante
  Quando tento consultar inscritos de uma atividade que não é minha
  Então o acesso é negado
```
