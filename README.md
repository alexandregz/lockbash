lockbash
========

Ruby script to change new terminals to the directory defined dir in .lockbash file (default ENV['HOME']+'/.lockbash')


Usage
=====

$ ./lockbash (to PATH_TO_DIR|remove|show)

Params:
```
to PATH_TO_DIR
  Directory to being locked
```
```
remove
  Removes lock
```
```
show
  Infor
```



Example:

```
alex@vostok:/Volumes/HD/dev/lockbash(master)$ ./lockbash show
No locked
alex@vostok:/Volumes/HD/dev/lockbash(master)$ ./lockbash to ~/Development/vagrant/
Locked to /Users/alex/Development/vagrant
alex@vostok:/Volumes/HD/dev/lockbash(master)$ ./lockbash show
Locked to /Users/alex/Development/vagrant
alex@vostok:/Volumes/HD/dev/lockbash(master)$ ./lockbash remove
Lockbash removed
alex@vostok:/Volumes/HD/dev/lockbash(master)$ ./lockbash show
No locked
alex@vostok:/Volumes/HD/dev/lockbash(master)$
````

New shell (locked to ~/Development/vagrant):
```
Last login: Sat Jan 31 00:07:56 on ttys003
Locked to /Users/alex/Development/vagrant
alex@vostok:~/Development/vagrant$
```

Howto
=====

Script only puts some bash code at .bash_profile to ```cd``` locked directory, like that:

```
# lock bash
LOCK_FILE=#LOCK_FILE#/.lockbash

if [ -f $LOCK_FILE ]; then
  DIR_TO_LOCK=$(cat $LOCK_FILE)
  eval REALPATH=$DIR_TO_LOCK  # to expand "~/dir", for example

  if [ -d $REALPATH ]; then
    cd $REALPATH
    echo "Locked to $DIR_TO_LOCK"
  fi
fi
```

With ```remove``` option, script deletes lockbash file and it removes code from .bash_profile file.
