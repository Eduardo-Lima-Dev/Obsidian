Em `_buildUpdateData`, os arrays usam checagem por truthiness (`if (dto.alergias) ...`). Além de não diferenciar bem “campo ausente” vs “campo presente como []”, isso fica especialmente problemático quando o DTO de PATCH aplica defaults. Prefira checar presença (`dto.alergias !== undefined`, ou `'alergias' in dto`) para que PATCH só altere arrays quando o cliente enviar o campo.

---

`findUnique` só aceita filtros por campos/índices únicos. `where: { id, ativo: true }` não é válido no Prisma (o modelo `Paciente` não tem chave única composta com `ativo`), então isso não compila/funciona. Use `findFirst({ where: { id, ativo: true } })` ou `findUnique({ where: { id } })` seguido de checagem de `ativo`.

This issue also appears on line 199 of the same file.

---

When a token has `role: 'doctor'` but `medico_id` is null, `effectiveMedicoId` becomes null and this `where` clause omits the doctor filter, so that user can list every active patient. Because `JwtPayload.medico_id` is nullable, this path should fail closed instead of dropping the row-level restriction.

This issue also appears on line 282 of the same file.

---

`PatchPatientSchema = UpdatePatientSchema.partial()` herda `.default(false)` e `.default([])` do schema de PUT. Com `nestjs-zod`, defaults são aplicados quando o campo não vem no body, então um PATCH vazio tende a sobrescrever `doador_orgaos`/`requer_acompanhante` para `false` e arrays para `[]` (perdendo dados). Para PATCH, remova defaults e deixe campos realmente opcionais, ou crie um schema separado (sem `.default`) e trate explicitamente a presença do campo.

---

The new patient response mapper no longer exposes `user_id`, even though the previous patient create response returned it and the analogous doctors API still includes `user_id`. Because `create()` now returns this mapper, clients that need to correlate the Paciente row with its base User record lose that identifier despite the PR adding User/Paciente transactional creation.

---

No select de listagem, incluir `agendamentos` com `orderBy` + `take` em relação 1-N costuma gerar padrão N+1 no Prisma (uma consulta por paciente para buscar os 2 últimos agendamentos). Isso pode degradar bastante a performance do `GET /patients` conforme o volume cresce. Considere remover esse nested select da listagem e carregar os “últimos agendamentos” via consulta separada/batch ou endpoint dedicado.

---

The service now returns raw Prisma field names and nested `user.email` objects for patient responses. Other API responses in this codebase map Prisma fields to snake_case keys (for example `src/modules/doctors/doctors.service.ts:58-76` returns `user_id`, `clinica_id`, `consulta_online`, `created_at`), so this response shape is inconsistent and likely breaks clients expecting the established API convention.