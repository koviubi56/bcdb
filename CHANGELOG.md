# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.4.0] - 2023-04-24

## Added

- **! Added `Table.get_rows_generator(self: Self@Table, *, lock: bool = True) -> Generator[tuple, None, None]`, which is the same as the _old_ `get_rows`, but it's a generator** (i'm not sure if that helps with performance or not)
- `Table` now supports type hints with TypeVarTuple
- `Table.remove_row(self: Self@Table, where: Where, must_remove: bool = True, silence_warning: bool = False) -> bool` got a new argument: `silence_warnings`. If it's not passed, or False, a warning will be issued if multiple rows matched `where(row)`
- `Table.remove_rows(self: Self@Table, where: Where, must_remove: bool = True, *, limit: int = 1000) -> int` got a new argument: `must_remove`. See docstring for more info.

## Changed

- `Table.get_rows()` just simply returns `list(self.get_rows_generator(...))`, and issues a warning. (Internally `get_rows` isn't used)
- Now error messages contain both row and line numbers, to make them easily distinguishable (eg: `on row 3 (line 4)`)
- Made some miscellaneous fixes/changes to docstrings and error messages.

## Fixed

- `Table.attributes` now doesn't acquire the lock
- Fixed some docstrings referencing renamed functions

## [0.4.0-beta.1] - 2022-11-26

## Added

- **! Added `Table.get_row_where(self: Self@Table, attribute_name: str, attribute_value: Any) -> tuple[Any, ...]`.**
- **! Added `Table.get_rows_where(self: Self@Table, attribute_name: str, attribute_value: Any, allow_empty: bool = False) -> list[tuple[Any, ...]]`.**

## [0.3.0] - 2022-11-25

## Added

- **! Added `Table.contains(self: Self@Table, attribute_name: str, attribute_value: Any) -> bool`.**
- **! Added `Table.not_contains(self: Self@Table, attribute_name: str, attribute_value: Any) -> bool`.**
- **! Added `Table.map(self: Self@Table, func: (tuple[Any, ...]) -> (tuple[Any, ...] | None), *, write: bool = False) -> list[tuple[Any, ...]]`.**
- **! Added `Table.filter(self: Self@Table, func: (tuple[Any, ...]) -> bool, *, write: bool = False) -> list[tuple[Any, ...]]`.**
- **! Added `Table.contains_row(self: Self@Table, row: tuple[Any, ...]) -> bool`.**
- **! Added `Table.not_contains_row(self: Self@Table, row: tuple[Any, ...]) -> bool`.**
- Added `Table.add_rows(self: Self@Table, rows: Iterable[tuple[Any, ...]], *, lock: bool = True) -> None`.
- Added `Table.get_attribute_index(self: Self@Table, name: str) -> int`.

## Fixed

- **Fixed problem with writing `\n` and `\r` to database.**
- `Database.add_table` checks that the table's name is unique, and its attributes' names are unique.

## [0.2.0] - 2022-11-19

## Added

- **! Added `Table.remove_row(self: Self@Table, where: Where, must_remove: bool = True) -> bool`.**
- **! Added `Table.remove_rows(self: Self@Table, where: Where, *, limit: int = 1000) -> int`.**
- **Added `Database.get_table(self: Self@Database, table_name: str) -> Table` which returns an existing table.**
- Added `Table.write_rows(self: Self@Table, rows: list[tuple[Any, ...]], *, i_know_what_im_doing: bool = False) -> None`. Usage is discouraged!
- Added argument `lock` to `Table.add_row`. Don't change it!

## [0.1.1] - 2022-11-18

## Added

- If the `directory` argument to `Database()` is a string, it will be converted to `pathlib.Path`.

## [0.1.0] - 2022-11-17
