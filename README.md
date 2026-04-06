# yandex_practicum_project_work_module_6

Проектная работа модуля 6 курса Yandex Practicum: рефакторинг кода на Rust.

## Ссылки на коммиты

- Исходная версия проекта (без изменений): <https://github.com/leo-millenial/yandex_practicum_project_work_module_6/commit/703fa75>
- Версия после рефакторинга: <https://github.com/leo-millenial/yandex_practicum_project_work_module_6/commit/890cd93>

## Что сделано

- Добавлен baseline-коммит с оригинальным проектом из `analysis-project.zip`.
- `read_log` переписан на дженерики (`R: Read`) без `Rc<RefCell<Box<dyn ...>>>` и без `unsafe`.
- Режимы чтения заменены с `u8 + if/else` на `enum ReadMode + match`.
- Убран `panic!` из библиотечного кода (ошибка режима теперь `ReadModeError`, есть `TryFrom<u8>`).
- Парсеры переведены на заимствования: `parse(&str) -> Result<(&str, T), ()>` вместо `String`.
- В `stdp::U32` применён tight-подход через `std::num::NonZeroU32`.
- Удалён singleton `LOG_LINE_PARSER`, добавлен обычный `parse_log_line`.
- Серия дублирующих `just_parse_*` заменена на единый generic helper `just_parse<T>`.
- Уменьшен размер данных в `AuthData` (перенос массива в heap через `Box<[u8; 1024]>`).

## Проверка

```bash
cargo test -- --nocapture
cargo test test_all -- --nocapture
cargo run example.log
```
