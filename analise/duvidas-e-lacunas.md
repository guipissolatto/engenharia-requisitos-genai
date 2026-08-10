# Dúvidas e Lacunas

Organizei este arquivo como um **roteiro para a próxima rodada de elicitação**: cada dúvida tem um stakeholder responsável por respondê-la, o impacto de deixá-la em aberto e, quando fez sentido, opções para apresentar na conversa (é mais fácil o stakeholder escolher entre alternativas do que responder uma pergunta aberta).

## Contradições encontradas

**C1 — Comprovante imediato × confirmação de pagamento.**
Os participantes querem "receber um comprovante logo após a inscrição", mas a equipe financeira diz que precisa "confirmar os pagamentos antes de liberar determinadas inscrições". Em um evento pago, o que o participante recebe logo após se inscrever, se a inscrição ainda não está confirmada? Minha proposta de conciliação: enviar imediatamente um comprovante de *solicitação* de inscrição, e um segundo comprovante de *confirmação* quando o pagamento for aprovado. Precisa ser validado com os dois grupos.

**C2 — "Vários workshops no mesmo dia" × "workshops no mesmo horário são simultâneos".**
O participante quer se inscrever em vários workshops do mesmo dia; o organizador diz que workshops no mesmo horário ocorrem simultaneamente. As duas falas convivem se — e só se — o sistema controlar sobreposição de horários. Ninguém disse isso explicitamente (ver RN08).

## Perguntas por stakeholder

### Para os organizadores

| ID | Pergunta | Impacto se ficar em aberto |
|----|----------|---------------------------|
| D01 | Até quando o participante pode cancelar a inscrição? (Opções para discutir: até X dias antes do evento; até o início; sem limite) | Bloqueia os critérios de aceitação do cancelamento (HU04) |
| D03 | Como funciona a lista de espera? Quando abre uma vaga: o primeiro da fila é inscrito automaticamente, ou recebe um convite com prazo para aceitar? Em evento pago, ele tem quanto tempo para pagar? | Bloqueia a especificação da lista de espera (HU08) e afeta o controle de vagas |
| D07 | O sistema deve bloquear inscrição em atividades com horários sobrepostos, apenas alertar, ou permitir? | RN08 é inferência minha; sem confirmação, o comportamento do sistema é indefinido |
| D10 | O que "gerenciar participantes" inclui na prática? (cancelar inscrição de terceiro? transferir? fazer check-in?) | RF12 fica vago demais para especificar |

### Para a equipe financeira

| ID | Pergunta | Impacto se ficar em aberto |
|----|----------|---------------------------|
| D02 | Em quais situações há reembolso? Integral ou parcial? Depende da antecedência do cancelamento? | Bloqueia os cenários de reembolso (HU05) |
| D06 | A vaga fica reservada quando o participante inicia o pagamento ou só após a confirmação? Se reservada, por quanto tempo? | Decisão central do domínio: muda o controle de vagas, a lista de espera e o estado "pendente de pagamento" (ver ciclo de vida da inscrição) |
| D09 | A confirmação de pagamento será manual (a equipe confirma no sistema) ou integrada a um meio de pagamento? | Muda o escopo técnico e o fluxo da inscrição paga |

### Para organizadores + financeiro em conjunto

| ID | Pergunta | Impacto se ficar em aberto |
|----|----------|---------------------------|
| D04 | O certificado é liberado automaticamente após o evento ou depende de presença registrada? Se depende, como a presença é registrada? | Bloqueia HU06; se houver controle de presença, surge um requisito funcional novo (check-in) que ninguém levantou |
| D05 | Por qual canal serão enviados comprovantes e notificações (e-mail? outro)? | RF03 e RF18 não têm como ser especificados por completo |

### Para o palestrante + jurídico/DPO

| ID | Pergunta | Impacto se ficar em aberto |
|----|----------|---------------------------|
| D08 | Quais dados dos inscritos o palestrante pode ver? (Proposta conservadora: nome e instituição, nada de contato) | Risco de conformidade com a LGPD; bloqueia parte da HU09 |

Sobre a última linha: o documento de elicitação não lista jurídico/compliance entre os stakeholders, mas a pergunta D08 (e o RNF04) não tem como ser respondida só por quem foi entrevistado. Sugiro incluir esse papel na próxima rodada.
