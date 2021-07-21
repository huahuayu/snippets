[//title]: (mysql-unix-timestamp-to-readable-utc-time-to-tz-time)
[//englishtitle]: (mysql-unix-timestamp-to-readable-utc-time-to-tz-time)
[//category]: (sql,mysql,snippet)
[//tags]: (sql,mysql,unix-timestamp,snippet)
[//createtime]: (20210629)
[//updatetime]: (20210629)

## one

unix time in db, select as it is

```sql
select tx_hash, block_number, block_timestamp as block_time from t_arb where tx_hash = "0x9156666e2146f6a3c700e1eab90d374e8a332cec41490bac558700a4005fbba2"
```

result:

| tx_hash                                                            | block_number | block_time |
| ------------------------------------------------------------------ | ------------ | ---------- |
| 0x9156666e2146f6a3c700e1eab90d374e8a332cec41490bac558700a4005fbba2 | 8719435      | 1624970377 |

## two

convert unix time to human readable datetime(in UTC) by `FROM_UNIXTIME()` function

```sql
select tx_hash, block_number, FROM_UNIXTIME(block_timestamp) as block_time from t_arb where tx_hash = "0x9156666e2146f6a3c700e1eab90d374e8a332cec41490bac558700a4005fbba2";
```

result:

| tx_hash                                                            | block_number | block_time          |
| ------------------------------------------------------------------ | ------------ | ------------------- |
| 0x9156666e2146f6a3c700e1eab90d374e8a332cec41490bac558700a4005fbba2 | 8719435      | 2021-06-29 12:39:37 |

## three

a step further, convert UTC time to your timezone datetime by `CONVERT_TZ()` function

```sql
select tx_hash, block_number, CONVERT_TZ(FROM_UNIXTIME(block_timestamp),'+00:00','+08:00') as block_time from t_arb where tx_hash = "0x9156666e2146f6a3c700e1eab90d374e8a332cec41490bac558700a4005fbba2";
```

result:

| tx_hash                                                            | block_number | block_time          |
| ------------------------------------------------------------------ | ------------ | ------------------- |
| 0x9156666e2146f6a3c700e1eab90d374e8a332cec41490bac558700a4005fbba2 | 8719435      | 2021-06-29 20:39:37 |
