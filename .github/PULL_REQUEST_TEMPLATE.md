<!--
  🏛️ Pull Request — finvix-governance
  Variante de la organización que GOBIERNA, no de las que entregan. No es el template de producto
  recortado: pregunta otras cosas, porque el riesgo es otro.

  • Aquí no se despliega nada, y el `apply` corre en CI al mergear. Sin segunda aprobación salvo en un destroy,
    que espera a leads con el plan delante — mergear ES aplicar. Por eso este template no exige un plan de rollback de despliegue,
    sino EL PLAN: el objeto sobre el que se decide, ANTES del merge (`docs/plano-de-control.md`).
  • Estos repos aplican estado: cada merge a `master` saca su tag `vX.Y.Z` y su release, sin rama de
    release ni hotfix. UNA sola rama, `master` (`docs/branches.md`).
  • Revisión: @finvix-governance/leads, vía CODEOWNERS, pero el ruleset no exige aprobación: el PR la
    abre la cuenta del dueño, que no puede aprobar lo suyo. Y quien escribe es `OrganizationAdmin` y
    bypassa el ruleset entero: la revisión NO es una puerta, es un rastro. Lo que la sustituye como
    control es que el plan esté publicado y que la deriva lo compruebe (`docs/plano-de-control.md`).
  • Merge = squash, único método permitido.
  • Labels: los de avisos (`warn/*`) los pone quien revisa cuando aplican; el resto los pone Dependabot
    o la automatización. Ningún proceso los lee para publicar.
  • Ninguna sección se borra: todas se llenan. Lo que no aplica se deja y se marca N/A —si el cambio
    no toca datos personales, la casilla de PII sigue ahí, marcada N/A—.
-->

## 🧭 Tracking

- **Referencia**: `#<n>`, el issue de este repositorio — `Closes #<n>` si este PR lo resuelve,
  `Ref #<n>` + por qué sigue abierto si no. `PEG-XXX` si además hay ticket de Jira.
- [ ] 🎫 **N/A** — este cambio no tiene issue: lo levanta la propia gobernanza

> 🔒 Rastrear no es opcional; el rastreador, sí. La clave `PEG` es **convención, no candado** —ningún
> ruleset la exige— y en estos tres repos el rastro vive en el
> buzón de Issues, no en el board.

## 📖 Qué cambia y por qué

<!-- La intención y el diseño. Si el cambio corrige algo que el repo decía y era falso, dilo aquí:
     un documento que ya no describe la realidad es un defecto, no una mejora pendiente. -->

## 🧾 El plan, publicado

> 🔒 **Se decide sobre un plan, no sobre un rótulo.** Un plan que no está en el PR convierte la
> decisión en un trámite (`docs/plano-de-control.md`). Pega el `terraform plan` COMPLETO, no su
> resumen — si es largo, dentro de un `<details>`.

- [ ] 🧾 **Plan a la vista**: el que CI publica en este PR, o pegado abajo si no corrió; o **N/A** — este
      cambio no toca el IaC de ninguna organización

<details><summary><code>terraform -chdir=orgs/&lt;org&gt; plan</code></summary>

```
<!-- aquí -->
```
</details>

- **Cifra exacta**: `_ to add, _ to change, _ to destroy`
- **Aislamiento** — los roots que este cambio NO pretende tocar salen sin **ningún** cambio de
  recurso. Un `Changes to Outputs` solo no es fallo: es la deriva de fondo ya medida.

### 🔴 Criterios de parar

Si alguno aparece en el plan, **no se aplica** y el PR no se mergea:

- [ ] `github_repository_environment` en **destroy** o **replace** — guarda la única copia de sus
      secrets, y GitHub los destruye con él. **Irreversible.**
- [ ] `github_repository_file.semilla` con el `content` **cambiado** — su contenido es del repo destino, no
      de `canonical/`. Se lee del plan en JSON, no del resumen.
- [ ] Cualquier destructivo que el plan **no había predicho**.

## 📐 Las cinco medidas

> 🔒 Sin las cinco, el cambio no se mergea. Si el cambio es solo documentación, la
> línea base y la meta son el estado del documento: qué decía que era falso y qué dice ahora.

| | |
|---|---|
| **Línea base** | <!-- el número de ANTES, medido --> |
| **Meta** | <!-- el número de DESPUÉS --> |
| **Comando de comprobación** | <!-- el que cualquiera puede correr para verificarlo --> |
| **Criterio de fallo** | <!-- qué resultado significa que salió mal --> |
| **Coste** | escrituras **ajenas**: `_` · propias: `_` · llamadas a la API: `_` · minutos de CI: `_` |

⚠️ **Las escrituras ajenas se cuentan aparte y a propósito.** Un commit dentro del repo de otro
equipo es lo único nuestro que ese equipo lee sin haberlo pedido. Si el número no es 0, justifica por
qué el cambio lo vale.

## ⚙️ El `apply`

- [ ] **No requiere `apply`** — solo documentación o scripts
- [ ] **Requiere `apply`, y se hace DESPUÉS del merge** — se aplica lo que se revisó
- [ ] **Ya aplicado**, y la comprobación de convergencia está abajo

## ✅ Verificado

<!-- Comandos y su salida REAL, no la esperada. "Debería pasar" no es una verificación. -->

- [ ] `terraform fmt -check -recursive` y `terraform validate` de cada root tocado — sin errores
- [ ] Lo que el cambio afirma, **medido**: el comando de la tabla de arriba, con su salida

## 🔗 Consistencia total

> 🔒 Un cambio que toca una convención toca **todos** sus documentos, en el mismo cierre. Lo que
> queda stale no es deuda: es el repo describiendo algo que no existe.

- [ ] `docs/` — el documento **dueño** del concepto, y los que lo enlazan
- [ ] El issue que este cambio cierra o mueve
- [ ] **N/A** — el cambio no toca ninguna convención

## 📚 Referencias

- 🔗 <!-- el documento dueño de la decisión, el runbook, la medición previa -->

---

> ✅ **Listo para revisión.** Revisor: **@finvix-governance/leads** vía CODEOWNERS.
> ⚠️ Recuerda que la revisión aquí **no bloquea a quien escribe** — el control real es el plan de
> arriba y la deriva semanal. Merge por **squash**, contra **`master`**, que es la única rama.
