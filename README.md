# Redis Data Types


## Keys
Redis Keys are:<br/>1. Unique. <br/>2. Binary Safe. Ex: "foo", 42, 3.14, 0xff <br/>3. Key names can be upto 512 MB. <br/>4. Length versus Readability.
```redis
127.0.0.1:6379> set paasapi "PaasAPI password"
OK
127.0.0.1:6379> get paasapi
"PaasAPI password"

127.0.0.1:6379> set paasapi PaasAPI_Password
OK
127.0.0.1:6379> get paasapi
"PaasAPI_Password"


Keys:
127.0.0.1:6379> keys paas*
1) "paasapi"
2) "paasui"

Scan:
127.0.0.1:6379> scan 0 match paas*
1) "0"
2) 1) "paasapi"
   2) "paasui"
   

127.0.0.1:6379> del paasapi #Blocking Command
(integer) 1
127.0.0.1:6379> KEYS paas*
1) "paasui"


127.0.0.1:6379> unlink paasui #UnBlocking Command
(integer) 1
127.0.0.1:6379> KEYS paas*
(empty array)


Key EXISTS(XX) & NOT EXISTS(NX):
127.0.0.1:6379> set inventory 1000 NX
OK
127.0.0.1:6379> set inventory 1111 NX
(nil)
127.0.0.1:6379> get inventory
"1000"
127.0.0.1:6379> set inventory 1111 XX
OK
127.0.0.1:6379> set inventory 5555 XX
OK
127.0.0.1:6379> get inventory
"5555"
127.0.0.1:6379> set inventory1 5555 XX
(nil)
127.0.0.1:6379> get inventory1
(nil)
```

There are two ways to get the keys:
| Keys: | Scan:  |
| :---:   | :-: |
| Blocks Until Complete | Iterates using a cursor |
| Never use in production | Returns a slot reference |
| Useful for debugging | May return 0 or more keys per call |
| | Safe for Production |



## Strings
## Hashes
## Lists
## Sets
## Sorted Sets

