# Bash
Bash reminders, tips, tricks and things I've forgot.

## STDERR & STDOUT
When using `>> output.txt`, it will only include STDOUT (Standard Output). To include errors with the output use:

- `>> output.txt 2>&1`

## For Loop
```bash
for i in $(ls *.*)
do;
  mv $i prefix_$i;
done
```

**or as a one-liner:** `for i in $(ls *.*) do; mv $i prefix_$i; done`

## For Loop in Range of Numbers
```bash
for i in {1..450}
do
wget http://hostname.fqdn:8081/$i -O /dev/null
sleep 1
done
```

**or as a one-liner:** `for i in {1..450}; do wget http://hostname.fqdn:8081/$i -O /dev/null; sleep 1; done`

## Multi-line Append
```bash 
cat >> /path/to/existingFile.text<< EOF
some text line 1
some text line 2
some text line 3
EOF
```

## Users and Groups

### Create a new user
```bash
useradd [options] [user_name]
```

### Assign/Change a password for a user
```bash
passwd [user_name]
```

### Add a User to a Group
```bash
usermod -a -G [group_name] [user_name]
```
