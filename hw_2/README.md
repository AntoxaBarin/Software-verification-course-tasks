## Домашнее задание №2


### Сборка
```bash
make
```

### Показ покрытия кода
```bash
make coverage
```

### Флаги компиляции

- `--O0`: Без оптимизаций, поскольку оптимизации могут изменять количество строк, а это скажется на измеряемом покрытии.

- `--coverage`, `-fprofile-arcs`, `-ftest-coverage`: просим компилятор собрать информацию, необходимую для подсчета покрытия.

- `-fno-inline`: не инлайним функции.

- `-fno-exceptions`: считаем, что функции не бросают исключений.

### MD/DC

Компилятор clang умеет вычислять MC/DC.

```bash
make clang
```
