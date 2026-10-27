# code-review-maintainability

> ¿Este cambio hace el código más barato o más caro de cambiar?

**Revisión de mantenibilidad** · Skill para agentes de código de la comunidad [nvvdev](https://github.com/nvv-dev). Funciona en Claude Code como plugin o como skill suelta, y en cualquier agente compatible con el formato abierto [`SKILL.md`](https://agentskills.io).

*English summary at the end.*

## Qué hace

Revisa la forma del código: archivos y funciones que crecen de más, condicionales que se repiten, módulos superficiales, capas que se mezclan, duplicación y nombres que no siguen el glosario. Prefiere tres comentarios de alta convicción a veinte cosméticos, y define cuándo aprobar.

## Objetivo

Frenar la complejidad que se acumula PR tras PR, sin convertir la revisión en una discusión de gustos.

## Cuándo usarla

- PRs grandes o refactorizaciones
- Revisiones periódicas de un módulo que cambia mucho

## Cuándo no

- Buscar bugs: usa code-review-deep
- Formato e imports: eso es del linter

## Ejemplo

```text
Haz una revisión de mantenibilidad de los cambios en src/billing.
```

## Cómo se activa

Esta skill **se activa sola**: Claude Code lee su descripción y la carga cuando la tarea coincide. También puedes pedirla por nombre ("usa la skill code-review-maintainability") o invocarla con `/code-review-maintainability:code-review-maintainability` (plugin) o `/code-review-maintainability` (copiada a `.claude/skills/`).

## Instalación

### Opción 1: Claude Code, como plugin (recomendada)

Dentro de Claude Code:

```text
/plugin marketplace add nvv-dev/claude-plugins
/plugin install code-review-maintainability@nvvdev
```

La primera línea agrega el catálogo de nvvdev una sola vez; la segunda instala esta skill. Si prefieres el paquete completo, instala `dev-workflow@nvvdev` en su lugar (incluye esta skill y las demás de [dev-workflow](https://github.com/nvv-dev/dev-workflow)); no instales los dos a la vez.

### Opción 2: Claude Code, copiando la skill

Para un solo proyecto (se comparte con tu equipo por git):

```bash
git clone --depth 1 https://github.com/nvv-dev/code-review-maintainability.git /tmp/code-review-maintainability
mkdir -p .claude/skills
cp -R /tmp/code-review-maintainability/skills/code-review-maintainability .claude/skills/
```

Para todos tus proyectos, cópiala en `~/.claude/skills/` en lugar de `.claude/skills/`.

### Opción 3: otros agentes

Copia la carpeta `skills/code-review-maintainability/` en la carpeta de skills de tu agente (cada agente documenta la suya). Con la CLI [skills](https://github.com/vercel-labs/skills) de Vercel Labs:

```bash
DISABLE_TELEMETRY=1 npx skills add nvv-dev/code-review-maintainability
```

### Verificar

Abre una sesión nueva y pregunta "¿qué skills tienes disponibles?"; `code-review-maintainability` debe aparecer. Con el plugin, `/plugin` la muestra como instalada.

### Actualizar o desinstalar

- Plugin: `/plugin marketplace update nvvdev` para actualizar; `/plugin uninstall code-review-maintainability@nvvdev` para quitarla.
- Copia manual: repite la copia para actualizar, o borra la carpeta `.claude/skills/code-review-maintainability`.

Antes de instalar cualquier skill, incluida esta, conviene leerla: es un solo archivo, [`skills/code-review-maintainability/SKILL.md`](skills/code-review-maintainability/SKILL.md). Ver [vetting-external-skills](https://github.com/nvv-dev/vetting-external-skills).

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/code-review-maintainability/SKILL.md` | La skill: instrucciones en inglés para que los escáneres de seguridad las analicen completas; el agente responde en tu idioma |
| `.claude-plugin/plugin.json` | Manifiesto para instalarla como plugin |
| `.github/workflows/` | Validación de estructura y escaneo con SkillSpector en cada cambio |

## Contribuir

Este repo se **genera** desde [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow), donde vive la versión canónica. Abre issues y PRs allí. La mejor contribución es un caso real en la sección *Known failures* de la skill, con la regla que lo evita.

## Origen

Escrita desde cero por nvvdev. Inspirada en: [cursor/plugins — thermos](https://github.com/cursor/plugins/tree/main/thermos) (maintainability rubric).

## Licencia

MIT.

---

## English

**code-review-maintainability** — Reviews shape, not bugs: size, branching, shallow modules, leaky layers; few high-conviction comments.

Install in Claude Code with `/plugin marketplace add nvv-dev/claude-plugins` and `/plugin install code-review-maintainability@nvvdev`, or copy `skills/code-review-maintainability/` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Other agents: copy the folder into their skills directory, or run `DISABLE_TELEMETRY=1 npx skills add nvv-dev/code-review-maintainability`. Loads automatically when the task matches its description. Canonical source: [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow). License: MIT.
