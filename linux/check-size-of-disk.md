

```bash
sudo lshw | grep -Pzo "\*-(disk|namespace)(\n.*)+?\s+size:.*?\(\K\d+\w+" | tr "\0" "\n" | paste -sd/
```
