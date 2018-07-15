## vimscript

### Presenting strings

```
echo "hello world!"
echom "hello world!"
```

**echom** will save the message in the message history.  

### Set Options

Use the keyword **set** to set the boolean options and integer options. For example:  

```
set number //show the index of the line
set numberwidth = 4
```

### Mapping

We use keyword **map** to set shortcut. For example:  

```
map - x //use - to delete the char behind the cursor
```

Use **<keyname>** to tell vim about special keys.  

```
map <space> viw
```

To map in different mode, use the following command:  

```
nmap //map in the normal mode, same as map
imap //map in the insert mode
vmap //map in the visual mode
```

**map** will executed recursively, for example:  

```
nmap - dd
nmap ¥ - //if u input ¥, then vim will execute dd
```

We can use noremap to deal with this issue:  

```
nnoremap ¥ x
```




