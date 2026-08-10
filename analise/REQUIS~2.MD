# Requisitos Não Funcionais

O documento de elicitação não trouxe nenhum requisito não funcional — isso inclusive está registrado nas observações ("não foram levantados requisitos relacionados à segurança, desempenho, disponibilidade, acessibilidade e privacidade dos dados").

Por isso, tudo neste arquivo é **proposta minha, ainda não validada com os stakeholders**. Preferi registrar candidatos com métricas concretas (mesmo que os números venham a mudar) a escrever coisas como "o sistema deve ser rápido e seguro", que não servem para teste nenhum. Os valores foram sugeridos pela IA e ajustados por mim; todos precisam ser confirmados na próxima rodada de elicitação.

| ID | Categoria | Proposta | Por que importa neste projeto |
|----|-----------|----------|-------------------------------|
| RNF01 | Segurança / acesso | Acesso autenticado com perfis distintos (participante, organizador, financeiro, palestrante), cada um vendo apenas o que seu papel exige. | O palestrante consulta dados de participantes e o financeiro lida com pagamentos — sem controle de perfil isso vira problema rápido. |
| RNF02 | Desempenho | O painel de inscritos do organizador deve refletir novas inscrições em até 10 segundos. | É a tradução verificável do "tempo real" pedido pelos organizadores. O número exato precisa ser combinado com eles. |
| RNF03 | Disponibilidade | O sistema deve suportar picos de acesso na abertura de inscrições de eventos concorridos sem perder inscrições nem vender vagas além do limite. | Abertura de inscrição é o momento crítico do domínio: muita gente disputando poucas vagas ao mesmo tempo. |
| RNF04 | Privacidade (LGPD) | Dados pessoais dos participantes tratados conforme a LGPD: coleta mínima, finalidade explícita e restrição do que cada perfil enxerga (em especial o palestrante — ver D08). | O sistema guarda dados pessoais e de pagamento; a elicitação nem tocou no assunto. |
| RNF05 | Acessibilidade | Interfaces públicas (catálogo, inscrição, emissão de certificado) seguindo WCAG 2.1 nível AA. | Eventos abertos ao público não podem excluir participantes com deficiência. |
| RNF06 | Usabilidade | Um participante deve conseguir completar uma inscrição sem instrução prévia. | A motivação do projeto foi justamente melhorar a experiência em relação a formulários e planilhas. |

Nota sobre concorrência: o RNF03 tem uma consequência funcional importante — duas pessoas não podem confirmar a última vaga ao mesmo tempo. Tratei o comportamento esperado no diagrama de ciclo de vida da inscrição (`especificacao/ciclo-de-vida-da-inscricao.md`).
