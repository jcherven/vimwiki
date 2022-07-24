# Bash Reminders

Some reminders and tips on using bash in ways that don't have inconsistent behavior or cause side effects on subsequent runs. 

## useful common command flags

### `mkdir`

mkdir's path flag wont exit the command with an error if the directory already exists. this doesn't overwrite the directory with a new one, it simply doesn't cause the script to stop.

```sh
mkdir -p raiseASuilen
```

### `ln`

ln will stop a script if the symlink already exists. passing the force flag prevents this by removing the target symlink and creating the intended symlink.

```sh
ln -sf source target
```

the `-no-dereference` flag is useful for symlinking directories. this will treat the link as a normal file if it's a symlink to a directory.

```sh
ln -sfn sourceDir targetDir
```

## `rm`

the `rm` force flag `-f` ignores non-existent files. however, this doesn't instruct `rm` to entirely avoid non-existent files.

