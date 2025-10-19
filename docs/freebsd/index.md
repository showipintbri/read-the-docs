# FreeBSD

## Mass File Rename
Will not RENAME only prints what would have been renamed.

```
foreach f (*Sound\ Clips\ and\ Quotes*)
    set new = `echo $f | sed 's/Sound\ Clips\ and\ Quotes/Audio\ Clips/g'`
    echo mv "$f" "$new"
end
```

To rename exclude the `echo` statement from the above.