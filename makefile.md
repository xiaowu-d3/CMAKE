# Syntax for makefile

Target: # dependency
<-tab-> command

- to don't print command when `make` => use @ before command

```makefile
hello: # hello world
    @echo "hello world this is my first make command"
```

```bash
# command makefile
make target_in_makefile
```

- To see all target in makefile:
- In makefile:

```makefile
help: # Show all commands
    @egrep -h '\s#\s' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?# "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'
```

- After:

```bash
make help
```

- if using `make` => execute a first command
- if not using target `help` in makefile, can use `.DEFAULT_GOAL = help` at top file => `make`
