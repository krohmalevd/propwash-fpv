# Codex guidance: Propwash FPV Russian localization

This repository is the user's fork of LardTom/propwash-fpv. The current work is an **incremental Russian (ru_ru) translation**, not a redesign of the mod. Follow `CONTRIBUTING.md`, `LICENSE`, and existing repository conventions. Give task reports in Russian.

## Repository map

- English source of truth: `common/src/lang/<module>/en_us.json`.
- German reference for context: `common/src/lang/<module>/de_de.json`.
- Editable Russian translations: `common/src/lang/<module>/ru_ru.json`.
- Merged, tracked game resource: `common/src/main/resources/assets/propwash/lang/ru_ru.json`.
- `:common:mergeLang` generates the merged resource. **Never edit it manually**; include its generated changes in localization commits.
- `common` is shared by Fabric and NeoForge. Minecraft 26.3 builds require **JDK 25**.

## Working rules

1. Work only on the modules and translation keys specified in the current task. Do not translate extra keys merely because they share the same file. Partial `ru_ru.json` files are expected during the project.
2. Preserve previously translated entries unchanged unless the task explicitly requests corrections. Do not modify English/German translations.
3. Keep JSON keys identical to the corresponding English keys; translate **values only**. Preserve placeholders (`%s`, `%1$s`, `%2$s`, `%%`, etc.), positional argument semantics, escaping, `\\n`, formatting codes, and meaningful whitespace (including leading spaces).
4. Write natural, concise Russian suited to Minecraft UI and real FPV terminology. Prefer short labels where space is limited; check context instead of translating words in isolation. Avoid literal, awkward machine translations.
5. Keep protocol names, item/part identifiers, commands, player-provided names, measurements, and units intact where appropriate.
6. Do **not** change Java code, physics, flight dynamics, network protocol, resource assets, Gradle configuration, or workflows unless the task explicitly requests such changes. If you discover hardcoded English text or a UI limitation, report it for a separate task.
7. Avoid re-auditing the entire repository in every task. Inspect only relevant files and their immediate context. Respect any pre-existing uncommitted changes; never discard unrelated work.
8. Do not create pull requests, publish builds/releases, or push to the upstream author's repository. Create commits and push to the user's fork only when explicitly requested by the task.

## FPV terminology guide

| English | Preferred Russian |
| --- | --- |
| Drone | Дрон |
| Drone Workbench | Верстак дронов |
| Frame | Рама |
| Flight controller | Полётный контроллер |
| FC/ESC stack | Полётный контроллер / ESC (shorten if UI space requires it) |
| Motor | Мотор |
| Propeller | Пропеллер |
| Battery | Аккумулятор |
| Video system | Видеосистема |
| Roll / Pitch / Yaw | Крен / Тангаж / Рысканье |
| Throttle | Газ |
| Hover throttle | Газ висения |
| Rates | Рейты |
| Thrust-to-weight ratio | Тяговооружённость |
| Dry weight | Масса без аккумулятора |
| All-up weight | Полная масса |
| Top speed | Максимальная скорость |
| Flight time | Время полёта |
| Save & close | Сохранить и закрыть |

Keep **FPV, ESC, OSD, PID, Acro, Angle, Horizon, GPS Rescue, Betaflight**, and standard technical identifiers when conventional. Translate arm/disarm based on the precise flight context; do not translate `armed` literally as `вооружён`. Prefer consistent wording across modules; flag genuinely ambiguous terms in your report.

## Validation and delivery

- Verify JSON parses, exactly the intended keys were added/changed, no duplicates exist, and placeholders and meaningful whitespace match the English originals.
- With JDK 25, run `./gradlew :common:mergeLang --configure-on-demand --console=plain` (Windows: `.\\gradlew.bat`). Check the generated `ru_ru.json` and expected cumulative key count. Missing-key warnings are normal during incremental translation.
- Review `git diff --check` and `git status`. Ensure unrelated dictionaries and source code remain untouched.
- If builds fail because dependencies cannot be downloaded, report the precise failure; **do not** change dependencies or build scripts to hide it.
- For each completed task, report: modules, translated key count, validation, changed files, remaining untranslated UI within the scope, commit SHA, and whether a push succeeded. Do not claim tests ran when they did not.
