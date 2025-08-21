- Sempre que tenta lançar uma Diaria do tipo Cama a tela fica Branca, mas adiciona em Itens
---

- **Correção:** A causa era o acesso a _dataEdit.nome_ quando _dataEdit_ está _Undefined_ ao lançar “Cama extra”. Ajustei o overlay para usar selectedType e dataEdit?.nome. (selectedType === 'Cama extra' || dataEdit?.nome === 'Cama')
- Ao tentar editar a quantidade de um Item (Cama), recebi um erro
- Recebi o mesmo erro ao tentar mudar de Cama para Diaria
---

- **Correção:** Adicionei um _normalizeDecimal,_ para garantir o . como separador decimal.