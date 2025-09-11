- Sempre que tenta lançar uma Diaria do tipo Cama a tela fica Branca, mas adiciona em Itens
---

- **Correção:** A causa era o acesso a _dataEdit.nome_ quando _dataEdit_ está _Undefined_ ao lançar “Cama extra”. Ajustei o overlay para usar selectedType e dataEdit?.nome. (selectedType === 'Cama extra' || dataEdit?.nome === 'Cama')
- Ao tentar editar a quantidade de um Item (Cama), recebi um erro
- Recebi o mesmo erro ao tentar mudar de Cama para Diaria
---

- **Correção:** Adicionei um _normalizeDecimal,_ para garantir o . como separador decimal.

graph TD
    A[09:00 - Cron Job] --> B{É dia 12 ou 18?}
    B -->|NÃO| C[Fim - Não envia]
    B -->|SIM| D[Buscar emails ativos]
    D --> E{Existem emails ativos?}
    E -->|NÃO| F[Log: Nenhum email configurado]
    E -->|SIM| G[Buscar coordenadores]
    G --> H{Existem coordenadores?}
    H -->|NÃO| I[Log: Nenhum coordenador encontrado]
    H -->|SIM| J[Para cada email configurado]
    J --> K{Já foi enviado hoje?}
    K -->|SIM| L[Pular este email]
    K -->|NÃO| M[Para cada coordenador]
    M --> N{Tem email válido?}
    N -->|NÃO| O[Pular coordenador]
    N -->|SIM| P[Enviar email]
    P --> Q[Log: Email enviado]
    Q --> R[Atualizar último envio]
    R --> S[Fim]