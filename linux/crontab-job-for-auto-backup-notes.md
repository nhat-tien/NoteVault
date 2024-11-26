
```
*     *     *     *     *     command to be executed
-     -     -     -     -
|     |     |     |     |
|     |     |     |     +----- day of week (0 - 6) (Sunday=0)
|     |     |     +------- month (1 - 12)
|     |     +--------- day of month (1 - 31)
|     +----------- hour (0 - 23)
+------------- min (0 - 59)
```


| Field | Giải thích       | Giá trị cho phép          |
|-------|------------------|---------------------------|
| MIN   | phút             | 0 to 59                   |
| HOUR  | Giờ              | 0 to 23                   |
| DOM   | Ngày trong tháng | 1-31                      |
| MON   | Tháng            | 1-12                      |
| DOW   | Ngày trong tuần  | 0-6                       |
| CMD   | Lệnh             | Các lệnh có thể thực hiện |


## Example

Chạy script 30 phút 1 lần

```bash
30 * * * * command
```

Chạy script vào 3 giờ sáng mỗi ngày

```bash
0 3 * * * command
```
