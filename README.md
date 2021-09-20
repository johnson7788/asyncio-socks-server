# asyncio-socks-server


A SOCKS proxy server implemented with the powerful python cooperative concurrency framework **asyncio**. 

## Features

- Supports both TCP and UDP with the implementation of SOCKS5 protocol
- Supports username/password authentication
- Provides optional strict mode that follows [RFC1928](https://www.ietf.org/rfc/rfc1928.txt) and [RFC1929](https://www.ietf.org/rfc/rfc1929.txt) without compromise
- Driven by the python standard library, no third-party dependencies

## Installation
Install with pip if Python 3.8.0 or higher is available.
```shell
pip install asyncio-socks-server
```

## Usage
When installed, you can invoke asyncio_socks_server from the command-line:
```shell
asyncio_socks_server [-h] [-v] 
                     [-H HOST] [-P PORT] [-A METHOD] 
                     [--access-logs] [--debug] [--strict] 
                     [--bind-addr BIND_ADDR]
                     [--env-prefix ENV_PREFIX]
                     [--config PATH]
```
where:

- `asyncio_socks_server`: You could use python -m asyncio_socks_server in development.
- `h`, `--help`: Show a help message and exit.
- `v`, `--version`: Show program's version number and exit.
- `-H HOST`, `--host HOST`: Host address to listen (default 0.0.0.0).
- `-P PORT`, `--port PORT`: Port to listen (default 1080).
- `-A METHOD`, `--auth METHOD`: Authentication method (default 0). 
  Possible values: 0 (no auth), 2 (username/password auth)
- `--access-logs`: Display access logs.
- `--debug`: Work in debug mode.
- `--strict`: Work in strict compliance with RFC1928 and RFC1929.
- `--bind-addr BIND_ADDR`: Value of BIND.ADDR field in the reply (default 0.0.0.0).
  It is not necessary for most clients.
  
If the value of METHOD is 2, that is, when the username/password authentication 
is specified, you need to provide a config file containing the user password 
in json format with `--config` option.
You can also list other options in the config file instead of the command：

`config.json:`
```json
{
  "LISTEN_HOST": "0.0.0.0",
  "LISTEN_PORT": 1080,
  "AUTH_METHOD": 2,
  "ACCESS_LOG": true,
  "DEBUG": true,
  "STRICT": true,
  "BIND_HOST": "0.0.0.0",
  "USERS": {
    "username1": "password1",
    "username2": "password2",
    "username3": "password3"
  }
}

```
```shell
asyncio_socks_server --config ${ENV}/config.json
```
In addition, any environment variable named starting with `AIOSS_` will also be applied 
to the config. 
You can also change the prefix by specifying `--env-prefix` option，for example:
```shell
export MY_LISTEN_HOST=127.0.0.1
export MY_LISTEN_PORT=8848

asyncio_socks_server --env-prefix MY_
```

## Reference
- [RFC1928](https://www.ietf.org/rfc/rfc1928.txt)
- [RFC1929](https://www.ietf.org/rfc/rfc1929.txt)
- [Anorov/PySocks](https://github.com/Anorov/PySocks)
- [Aber/socks5](https://github.com/Aber-s-practice/socks5)
- [Ehco1996/aioshadowsocks](https://github.com/Ehco1996/aioshadowsocks)
