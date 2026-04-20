# praia-redis

Redis client for [Praia](https://github.com/praia-lang/praia). Implements the RESP (REdis Serialization Protocol) using raw TCP sockets — no external C libraries required.

## Install

```bash
sand install github.com/viggou/praia-redis
```

## Usage

```
use "redis"

let r = redis.connect({
    host: "localhost",
    port: 6379,
    password: "secret"
})

r.set("name", "Ada")
print(r.get("name"))

r.del("name")
r.close()
```

## Config

| Field | Default | Description |
|-------|---------|-------------|
| `host` | `"localhost"` | Server hostname |
| `port` | `6379` | Server port |
| `password` | — | Password (optional) |
| `username` | — | Username for Redis 6+ ACL auth (optional) |
| `db` | `0` | Database number (optional) |

## API

`redis.connect(config)` returns a client with the following methods:

### Strings

| Method | Description |
|--------|-------------|
| `get(key)` | Get the value of a key |
| `set(key, value)` | Set a key to a value |
| `setnx(key, value)` | Set a key only if it does not exist |
| `getset(key, value)` | Set a key and return its old value |
| `mget(keys)` | Get values of multiple keys (pass an array) |
| `incr(key)` | Increment integer value by 1 |
| `incrby(key, amount)` | Increment integer value by amount |
| `decr(key)` | Decrement integer value by 1 |
| `decrby(key, amount)` | Decrement integer value by amount |
| `append(key, value)` | Append a value to a key |

### Keys

| Method | Description |
|--------|-------------|
| `del(key)` | Delete a key |
| `exists(key)` | Check if a key exists (returns 1 or 0) |
| `expire(key, seconds)` | Set a TTL in seconds |
| `ttl(key)` | Get remaining TTL in seconds |
| `persist(key)` | Remove the TTL from a key |
| `keys(pattern)` | Find keys matching a glob pattern |
| `rename(key, newkey)` | Rename a key |
| `type(key)` | Get the type of value stored at a key |

### Lists

| Method | Description |
|--------|-------------|
| `lpush(key, value)` | Prepend a value to a list |
| `rpush(key, value)` | Append a value to a list |
| `lpop(key)` | Remove and return the first element |
| `rpop(key)` | Remove and return the last element |
| `llen(key)` | Get the length of a list |
| `lrange(key, start, stop)` | Get a range of elements |
| `lindex(key, index)` | Get an element by index |

### Sets

| Method | Description |
|--------|-------------|
| `sadd(key, member)` | Add a member to a set |
| `srem(key, member)` | Remove a member from a set |
| `smembers(key)` | Get all members of a set |
| `sismember(key, member)` | Check if a value is in a set (returns 1 or 0) |
| `scard(key)` | Get the number of members in a set |

### Hashes

| Method | Description |
|--------|-------------|
| `hset(key, field, value)` | Set a hash field |
| `hget(key, field)` | Get a hash field value |
| `hdel(key, field)` | Delete a hash field |
| `hgetall(key)` | Get all fields and values as a map |
| `hexists(key, field)` | Check if a hash field exists (returns 1 or 0) |
| `hkeys(key)` | Get all field names in a hash |
| `hvals(key)` | Get all values in a hash |
| `hlen(key)` | Get the number of fields in a hash |

### Sorted Sets

| Method | Description |
|--------|-------------|
| `zadd(key, score, member)` | Add a member with a score |
| `zrem(key, member)` | Remove a member |
| `zscore(key, member)` | Get the score of a member |
| `zrank(key, member)` | Get the rank of a member |
| `zrange(key, start, stop)` | Get members in a range by rank |
| `zcard(key)` | Get the number of members |

### Pub/Sub

| Method | Description |
|--------|-------------|
| `publish(channel, message)` | Publish a message to a channel |

### Server

| Method | Description |
|--------|-------------|
| `ping()` | Ping the server (returns "PONG") |
| `echo(message)` | Echo a message back |
| `info()` | Get server info |
| `dbsize()` | Get the number of keys in the current database |
| `flushdb()` | Delete all keys in the current database |
| `flushall()` | Delete all keys in all databases |

### Raw

| Method | Description |
|--------|-------------|
| `raw(args)` | Send any command as an array (e.g. `r.raw(["CONFIG", "GET", "maxmemory"])`) |

### Connection

| Method | Description |
|--------|-------------|
| `close()` | Close the connection |

## License

MIT
