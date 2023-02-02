## Boo-Gen!

This has been folked from h0mbre's boo-gen and has a couple of slight changes that allow it to create a python script to fuzz over https

## Usage 

`boo-gen.py request.txt <method> <output filename(optional)>`

### Examples
`boo-gen.py get.txt --get -f fuzz.py`

`boo-gen.py post.txt --post -f fuzz.py`

## GET Requests

### Saved HTTP Request
```terminal_session
GET / HTTP/1.1
Host: 192.168.1.2:8006
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="109", "Not_A Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.120 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Connection: close
```

### Running Boo-Gen
```terminal_session
root@kali:~/ # python boo-gen.py get.txt --get
```

### Output (http.py)
```python
#!/usr/bin/env python
from boofuzz import *
#import multiprocessing
import ssl

def main():
    context = ssl.create_default_context()
    context.check_hostname = False
    context.verify_mode = ssl.CERT_NONE
    session = Session(
        target=Target(
            connection=SocketConnection("192.168.1.2",8006, proto='ssl', server=False, sslcontext=context, server_hostname="https://192.168.1.2:8006")
        ),
    )

    s_initialize(name="Request")
    with s_block("Request-Line"):
        s_group("Method", ["GET"])
        s_delim(" ", name='space-1', fuzzable = False)
        s_string("/", name='Request-URI', fuzzable = False)
        s_delim(" ", name='space-2', fuzzable = False)
        s_string("HTTP/1.1", name='HTTP-Version', fuzzable = False)
    s_delim("\r\n", name='return-1', fuzzable = False)
    s_string("Host:", name="Host", fuzzable = False)
    s_delim(" ", name="space-3", fuzzable = False)
    s_string("192.168.1.2:8006", name="Host-Value", fuzzable = False)
    s_delim("\r\n", name="return-2", fuzzable = False)
    s_string("Cache-Control:", name="Cache-Control", fuzzable = False)
    s_delim(" ", name="space-4", fuzzable = False)
    s_string("max-age=0", name="Cache-Control-Value", fuzzable = False)
    s_delim("\r\n", name="return-3", fuzzable = False)
    s_string("Sec-Ch-Ua:", name="Sec-Ch-Ua", fuzzable = False)
    s_delim(" ", name="space-5", fuzzable = False)
    s_string("'Chromium';v='109', 'Not_A Brand';v='99'", name="Sec-Ch-Ua-Value", fuzzable = False)
    s_delim("\r\n", name="return-4", fuzzable = False)
    s_string("Sec-Ch-Ua-Mobile:", name="Sec-Ch-Ua-Mobile", fuzzable = False)
    s_delim(" ", name="space-6", fuzzable = False)
    s_string("?0", name="Sec-Ch-Ua-Mobile-Value", fuzzable = False)
    s_delim("\r\n", name="return-5", fuzzable = False)
    s_string("Sec-Ch-Ua-Platform:", name="Sec-Ch-Ua-Platform", fuzzable = False)
    s_delim(" ", name="space-7", fuzzable = False)
    s_string("'Windows'", name="Sec-Ch-Ua-Platform-Value", fuzzable = False)
    s_delim("\r\n", name="return-6", fuzzable = False)
    s_string("Upgrade-Insecure-Requests:", name="Upgrade-Insecure-Requests", fuzzable = False)
    s_delim(" ", name="space-8", fuzzable = False)
    s_string("1", name="Upgrade-Insecure-Requests-Value", fuzzable = False)
    s_delim("\r\n", name="return-7", fuzzable = False)
    s_string("User-Agent:", name="User-Agent", fuzzable = False)
    s_delim(" ", name="space-9", fuzzable = False)
    s_string("Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.120 Safari/537.36", name="User-Agent-Value", fuzzable = False)
    s_delim("\r\n", name="return-8", fuzzable = False)
    s_string("Accept:", name="Accept", fuzzable = False)
    s_delim(" ", name="space-10", fuzzable = False)
    s_string("text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9", name="Accept-Value", fuzzable = False)
    s_delim("\r\n", name="return-9", fuzzable = False)
    s_string("Sec-Fetch-Site:", name="Sec-Fetch-Site", fuzzable = False)
    s_delim(" ", name="space-11", fuzzable = False)
    s_string("none", name="Sec-Fetch-Site-Value", fuzzable = False)
    s_delim("\r\n", name="return-10", fuzzable = False)
    s_string("Sec-Fetch-Mode:", name="Sec-Fetch-Mode", fuzzable = False)
    s_delim(" ", name="space-12", fuzzable = False)
    s_string("navigate", name="Sec-Fetch-Mode-Value", fuzzable = False)
    s_delim("\r\n", name="return-11", fuzzable = False)
    s_string("Sec-Fetch-User:", name="Sec-Fetch-User", fuzzable = False)
    s_delim(" ", name="space-13", fuzzable = False)
    s_string("?1", name="Sec-Fetch-User-Value", fuzzable = False)
    s_delim("\r\n", name="return-12", fuzzable = False)
    s_string("Sec-Fetch-Dest:", name="Sec-Fetch-Dest", fuzzable = False)
    s_delim(" ", name="space-14", fuzzable = False)
    s_string("document", name="Sec-Fetch-Dest-Value", fuzzable = False)
    s_delim("\r\n", name="return-13", fuzzable = False)
    s_string("Accept-Encoding:", name="Accept-Encoding", fuzzable = False)
    s_delim(" ", name="space-15", fuzzable = False)
    s_string("gzip, deflate", name="Accept-Encoding-Value", fuzzable = False)
    s_delim("\r\n", name="return-14", fuzzable = False)
    s_string("Accept-Language:", name="Accept-Language", fuzzable = True)
    s_delim(" ", name="space-16", fuzzable = False)
    s_string("en-GB,en-US;q=0.9,en;q=0.8", name="Accept-Language-Value", fuzzable = True)
    s_delim("\r\n", name="return-15", fuzzable = False)
    s_string("Connection:", name="Connection", fuzzable = False)
    s_delim(" ", name="space-17", fuzzable = False)
    s_string("close", name="Connection-Value", fuzzable = False)
    s_delim("\r\n", name="return-16", fuzzable = False)
    s_static("\r\n", name="Request-Line-CRLF")
    s_static("\r\n", "Request-CRLF")

    session.connect(s_get("Request"))

    session.fuzz()


if __name__ == "__main__":
    main()
```

## POST Requests

### Saved HTTP Request
```terminal_session
POST /api2/extjs/access/ticket HTTP/1.1
Host: 192.168.1.2:8006
Content-Length: 56
Sec-Ch-Ua: "Chromium";v="109", "Not_A Brand";v="99"
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Csrfpreventiontoken: null
X-Requested-With: XMLHttpRequest
Sec-Ch-Ua-Mobile: ?0
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.120 Safari/537.36
Sec-Ch-Ua-Platform: "Windows"
Accept: */*
Origin: https://192.168.1.2:8006
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://192.168.1.2:8006/
Accept-Encoding: gzip, deflate
Accept-Language: en-GB,en-US;q=0.9,en;q=0.8
Connection: close

username=root&password=H0rizonta7&realm=pam&new-format=1   

```

### Running Boo-Gen
```terminal_session
root@kali:~/ # python boo-gen.py post.txt --post
```

### Output (http.py)
```python
#!/usr/bin/env python

from boofuzz import *
#import multiprocessing
import ssl


def main():
    context = ssl.create_default_context()
    context.check_hostname = False
    context.verify_mode = ssl.CERT_NONE
    session = Session(
        target=Target(
            connection=SocketConnection("192.168.1.2",8006, proto='ssl', server=False, sslcontext=context, server_hostname="https://192.168.1.2:8006" )
        ),
    )

    s_initialize(name="Request")
    with s_block("Request-Line"):
        s_group("Method", ["POST"])
        s_delim(" ", name='space-1', fuzzable = False)
        s_string("/api2/extjs/access/ticket", name='Request-URI', fuzzable = False)
        s_delim(" ", name='space-2', fuzzable = False)
        s_string("HTTP/1.1", name='HTTP-Version', fuzzable = False)
    s_delim("\r\n", name='return-1', fuzzable = False)
    s_string("Host:", name="Host", fuzzable = False)
    s_delim(" ", name="space-3", fuzzable = False)
    s_string("192.168.1.2:8006", name="Host-Value", fuzzable = False)
    s_delim("\r\n", name="return-2", fuzzable = False)
    s_string("Content-Length:", name="Content-Length", fuzzable = False)
    s_delim(" ", name="space-4", fuzzable = False)
    s_string("56", name="Content-Length-Value", fuzzable = False)
    s_delim("\r\n", name="return-3", fuzzable = False)
    s_string("Sec-Ch-Ua:", name="Sec-Ch-Ua", fuzzable = False)
    s_delim(" ", name="space-5", fuzzable = False)
    s_string("'Chromium';v='109', 'Not_A Brand';v='99'", name="Sec-Ch-Ua-Value", fuzzable = False)
    s_delim("\r\n", name="return-4", fuzzable = False)
    s_string("Content-Type:", name="Content-Type", fuzzable = False)
    s_delim(" ", name="space-6", fuzzable = False)
    s_string("application/x-www-form-urlencoded; charset=UTF-8", name="Content-Type-Value", fuzzable = False)
    s_delim("\r\n", name="return-5", fuzzable = False)
    s_string("Csrfpreventiontoken:", name="Csrfpreventiontoken", fuzzable = False)
    s_delim(" ", name="space-7", fuzzable = False)
    s_string("null", name="Csrfpreventiontoken-Value", fuzzable = False)
    s_delim("\r\n", name="return-6", fuzzable = False)
    s_string("X-Requested-With:", name="X-Requested-With", fuzzable = False)
    s_delim(" ", name="space-8", fuzzable = False)
    s_string("XMLHttpRequest", name="X-Requested-With-Value", fuzzable = False)
    s_delim("\r\n", name="return-7", fuzzable = False)
    s_string("Sec-Ch-Ua-Mobile:", name="Sec-Ch-Ua-Mobile", fuzzable = False)
    s_delim(" ", name="space-9", fuzzable = False)
    s_string("?0", name="Sec-Ch-Ua-Mobile-Value", fuzzable = False)
    s_delim("\r\n", name="return-8", fuzzable = False)
    s_string("User-Agent:", name="User-Agent", fuzzable = False)
    s_delim(" ", name="space-10", fuzzable = False)
    s_string("Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.120 Safari/537.36", name="User-Agent-Value", fuzzable = False)
    s_delim("\r\n", name="return-9", fuzzable = False)
    s_string("Sec-Ch-Ua-Platform:", name="Sec-Ch-Ua-Platform", fuzzable = False)
    s_delim(" ", name="space-11", fuzzable = False)
    s_string("'Windows'", name="Sec-Ch-Ua-Platform-Value", fuzzable = False)
    s_delim("\r\n", name="return-10", fuzzable = False)
    s_string("Accept:", name="Accept", fuzzable = False)
    s_delim(" ", name="space-12", fuzzable = False)
    s_string("*/*", name="Accept-Value", fuzzable = False)
    s_delim("\r\n", name="return-11", fuzzable = False)
    s_string("Origin:", name="Origin", fuzzable = False)
    s_delim(" ", name="space-13", fuzzable = False)
    s_string("https://192.168.1.2:8006", name="Origin-Value", fuzzable = False)
    s_delim("\r\n", name="return-12", fuzzable = False)
    s_string("Sec-Fetch-Site:", name="Sec-Fetch-Site", fuzzable = False)
    s_delim(" ", name="space-14", fuzzable = False)
    s_string("same-origin", name="Sec-Fetch-Site-Value", fuzzable = False)
    s_delim("\r\n", name="return-13", fuzzable = False)
    s_string("Sec-Fetch-Mode:", name="Sec-Fetch-Mode", fuzzable = False)
    s_delim(" ", name="space-15", fuzzable = False)
    s_string("cors", name="Sec-Fetch-Mode-Value", fuzzable = False)
    s_delim("\r\n", name="return-14", fuzzable = False)
    s_string("Sec-Fetch-Dest:", name="Sec-Fetch-Dest", fuzzable = False)
    s_delim(" ", name="space-16", fuzzable = False)
    s_string("empty", name="Sec-Fetch-Dest-Value", fuzzable = False)
    s_delim("\r\n", name="return-15", fuzzable = False)
    s_string("Referer:", name="Referer", fuzzable = False)
    s_delim(" ", name="space-17", fuzzable = False)
    s_string("https://192.168.1.2:8006/", name="Referer-Value", fuzzable = False)
    s_delim("\r\n", name="return-16", fuzzable = False)
    s_string("Accept-Encoding:", name="Accept-Encoding", fuzzable = False)
    s_delim(" ", name="space-18", fuzzable = False)
    s_string("gzip, deflate", name="Accept-Encoding-Value", fuzzable = False)
    s_delim("\r\n", name="return-17", fuzzable = False)
    s_string("Accept-Language:", name="Accept-Language", fuzzable = False)
    s_delim(" ", name="space-19", fuzzable = False)
    s_string("en-GB,en-US;q=0.9,en;q=0.8", name="Accept-Language-Value", fuzzable = False)
    s_delim("\r\n", name="return-18", fuzzable = False)
    s_string("Connection:", name="Connection", fuzzable = False)
    s_delim(" ", name="space-20", fuzzable = False)
    s_string("close", name="Connection-Value", fuzzable = False)
    s_delim("\r\n", name="return-19", fuzzable = False)
    s_delim("\r\n", name="return-20", fuzzable = False)
    s_string("username", name="username-Param", fuzzable = False)
    s_delim("=", name="Equal-1", fuzzable = False)
    s_string("root", name="username-Value", fuzzable = False)
    s_delim("&", name="Ampersand-1", fuzzable = False)
    s_string("password", name="password-Param", fuzzable = False)
    s_delim("=", name="Equal-2", fuzzable = False)
    s_string("H0rizonta7", name="password-Value", fuzzable = False)
    s_delim("&", name="Ampersand-2", fuzzable = False)
    s_string("realm", name="realm-Param", fuzzable = False)
    s_delim("=", name="Equal-3", fuzzable = False)
    s_string("pam", name="realm-Value", fuzzable = False)
    s_delim("&", name="Ampersand-3", fuzzable = False)
    s_string("new-format", name="new-format-Param", fuzzable = False)
    s_delim("=", name="Equal-4", fuzzable = False)
    s_string("1", name="new-format-Value", fuzzable = False)
    s_delim("&", name="Ampersand-4", fuzzable = False)

    session.connect(s_get("Request"))

    session.fuzz()


if __name__ == "__main__":
    main()
```

