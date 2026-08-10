# Requisitos Funcionais

Levantei os requisitos abaixo a partir das falas registradas no documento de elicitação. Cada requisito indica de onde veio (qual stakeholder pediu). Quando o requisito depende de alguma definição pendente, aponto a dúvida correspondente (arquivo `duvidas-e-lacunas.md`).

## Participantes

| ID | Requisito | Origem | Pendências |
|----|-----------|--------|------------|
| RF01 | O sistema deve exibir um catálogo com todos os eventos disponíveis, com data, horário, local, valor e vagas. | "Gostaria de visualizar todos os eventos disponíveis em um único lugar." | — |
| RF02 | O sistema deve permitir que o participante se inscreva em um evento. | Contexto do projeto + falas dos participantes | D06 (momento da reserva da vaga) |
| RF03 | O sistema deve enviar um comprovante ao participante após a inscrição. | "Seria interessante receber um comprovante logo após a inscrição." | D05 (canal de envio); ver também a contradição C1 em `duvidas-e-lacunas.md` |
| RF04 | O sistema deve permitir que o participante cancele a própria inscrição, sem intermediação da organização, quando o evento permitir cancelamento. | "Gostaria de cancelar minha inscrição sem precisar entrar em contato com a organização." | D01 (prazo limite) |
| RF05 | O sistema deve permitir que o participante emita seu certificado após o evento. | "Quero conseguir emitir meu certificado depois do evento." | D04 (emissão automática ou condicionada à presença) |
| RF06 | O sistema deve permitir inscrição em mais de um workshop realizado no mesmo dia, desde que os horários não conflitem. | "Gostaria de me inscrever em vários workshops que acontecerão no mesmo dia." | D07 (tratamento de conflito de horário); C2 |
| RF07 | O sistema deve permitir que o participante acompanhe a situação das suas inscrições (confirmada, pendente de pagamento, em lista de espera, cancelada). | "acompanhar inscrições" (tabela de stakeholders) | — |

## Organizadores

| ID | Requisito | Origem | Pendências |
|----|-----------|--------|------------|
| RF08 | O sistema deve permitir que o organizador cadastre e edite eventos (congressos, workshops, eventos corporativos), incluindo limite de vagas, valor e política de cancelamento. | "Criar eventos, controlar vagas" | — |
| RF09 | O sistema deve controlar automaticamente o número de vagas, impedindo inscrições confirmadas além do limite. | "Precisamos controlar automaticamente o número de vagas." | D06 |
| RF10 | O sistema deve manter uma lista de espera quando o evento lotar. | "Quando um evento lotar, seria interessante criar uma lista de espera." | D03 (funcionamento da lista) |
| RF11 | O sistema deve exibir aos organizadores a quantidade de inscritos em tempo real. | "Gostaríamos de acompanhar a quantidade de inscritos em tempo real." | "tempo real" é vago — tratei em RNF02 |
| RF12 | O sistema deve permitir ao organizador gerenciar os participantes de um evento (consultar, e possivelmente cancelar/remanejar inscrições). | "gerenciar participantes" (tabela de stakeholders) | O que exatamente "gerenciar" inclui não foi detalhado (D10) |

## Equipe financeira

| ID | Requisito | Origem | Pendências |
|----|-----------|--------|------------|
| RF13 | O sistema deve suportar eventos gratuitos e pagos. | "Alguns eventos são gratuitos e outros exigem pagamento." | — |
| RF14 | O sistema deve registrar pagamentos e permitir que a equipe financeira os confirme. | "Precisamos confirmar os pagamentos antes de liberar determinadas inscrições." | Não foi dito se a confirmação é manual ou integrada a um gateway (D09) |
| RF15 | O sistema deve registrar solicitações de reembolso e sua resolução. | "Em alguns casos o participante tem direito ao reembolso, em outros não." | D02 (critérios de reembolso) |

## Palestrantes

| ID | Requisito | Origem | Pendências |
|----|-----------|--------|------------|
| RF16 | O sistema deve permitir ao palestrante consultar a programação das suas atividades. | Tabela de stakeholders | — |
| RF17 | O sistema deve permitir ao palestrante consultar a lista de participantes inscritos nas suas atividades. | "Gostaria de consultar a lista de participantes inscritos em minhas atividades." | D08 (quais dados podem ser exibidos — questão de privacidade) |

## Transversais

| ID | Requisito | Origem | Pendências |
|----|-----------|--------|------------|
| RF18 | O sistema deve enviar notificações aos participantes sobre eventos relevantes da sua inscrição (confirmação, convocação da lista de espera, cancelamento, liberação de certificado). | Derivado das observações do documento | D05 (canais) |

Uma observação: RF18 não foi pedido com essas palavras por ninguém — eu o derivei porque comprovante (RF03), lista de espera (RF10) e cancelamento (RF04) só funcionam na prática se o participante ficar sabendo do que aconteceu. Marquei como derivado para deixar claro que precisa ser validado.
