# Regras de Negócio

Separei as regras de negócio dos requisitos funcionais porque elas são restrições do negócio da Eventus — valem independentemente de como o sistema for construído. Muitas estão incompletas: a elicitação afirmou que a regra existe, mas não disse como ela funciona. Nesses casos a regra aparece aqui com a parte pendente marcada, e a pergunta correspondente está em `duvidas-e-lacunas.md`.

**RN01 — Limite de vagas.** Todo evento tem um número máximo de vagas, definido pelo organizador. Nenhuma inscrição pode ser confirmada acima desse limite.

**RN02 — Lista de espera.** Quando o evento lota, novos interessados entram em uma lista de espera. *Pendente:* como a vaga liberada é oferecida (automático? convite com prazo? ordem de chegada?) — D03.

**RN03 — Cancelamento é configurável por evento.** Nem todo evento permite cancelamento de inscrição. A política de cancelamento é uma propriedade do evento, definida na sua criação. *Pendente:* prazo limite para cancelar, quando permitido — D01.

**RN04 — Reembolso é condicional.** Em eventos pagos, o cancelamento pode ou não dar direito a reembolso, dependendo de condições que a equipe financeira não detalhou. *Pendente:* quais condições (antecedência? tipo de evento? percentual?) — D02.

**RN05 — Pagamento antes da confirmação.** Em eventos pagos, a inscrição só é confirmada após a confirmação do pagamento pela equipe financeira. Em eventos gratuitos, a confirmação é imediata (havendo vaga).

**RN06 — Reserva de vaga durante o pagamento.** *Totalmente pendente:* não foi definido se a vaga fica reservada quando o participante inicia o pagamento ou só quando ele é confirmado — D06. Essa decisão muda o comportamento do controle de vagas e da lista de espera, então preferi não assumir nada.

**RN07 — Certificado só depois do evento.** O certificado só pode ser emitido após a realização do evento. *Pendente:* se exige confirmação de presença — D04.

**RN08 — Conflito de horário.** Workshops que acontecem no mesmo horário ocorrem simultaneamente, e o participante quer se inscrever em vários no mesmo dia. Disso deduzi que o sistema deveria impedir (ou ao menos alertar sobre) inscrições em atividades com horários sobrepostos — mas **nenhum stakeholder afirmou isso diretamente**. Registrei como regra inferida, a validar — D07.

**RN09 — Visibilidade de dados pelo palestrante.** O palestrante só pode ver dados dos participantes das *suas* atividades. *Pendente:* quais dados (proponho restringir a nome e instituição até definição em contrário, por causa da LGPD) — D08.
