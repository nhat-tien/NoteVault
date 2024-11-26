`$@` : is the array of all the input parameters

```bash
i=1; 
for user in "$@" do 
echo "Username - $i: $user"; 
i=$((i + 1)); 
done
```

```bash
sh users-loop.sh john matt bill 'joe wicks' carol
```

```bash
Username - 1: john
Username - 2: matt
Username - 3: bill
Username - 4: joe wicks
Username - 5: carol
```

`$#` : returns the input size
