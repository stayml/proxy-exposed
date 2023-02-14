# proxy.exposed
A simple API to let you test proxy servers to determine [IP address](https://ipv4.icanhazip.com/) - and [other identifying information](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Request_fields) - exposure

## Example Response
**GET** http://proxy.exposed/?ip=22.33.44.55

    {
      "proxy": "elite",
      'headers': {
        'Host': 'proxy.exposed',
        'Connection': 'close',
        'User-Agent': 'python-requests/2.28.1',
        'Accept-Encoding': 'gzip, deflate, br',
        'Accept': '*/*'
        },
      "proxy_headers": {},
      "requesting_ip_address": "1.2.3.4",
      "real_ip_leak": false
    }
    
## Usage
Issue a  **GET**  request through your proxy server to the specified URL below _(there are two interfaces: `http` and `https`, depending on the capabilities of your proxy server)_  including the parameter  `ip`  set to your **true IP address**.

_Discover your ip address [here](https://ipv4.icanhazip.com/)_.

#### HTTP

    http://proxy.exposed/?ip=your.real.ip.address

#### HTTPS

    https://proxy.exposed/?ip=your.real.ip.address

Your request will be searched for any exposure of your true IP address and any match against a list of proxy-specific headers.

The results of the check and a classification of the requesting proxy will be returned.

### Using Python Requests

    import requests
    
    try:
        r = requests.get(
            'http://proxy.exposed', # http
            params = {
                'ip': '░░░.▒▒▒.███.▓▓' # replace with your ip
            }, 
            proxies = {
	            'http' : 'http://user:pass@proxy.server:5225'
            }
        )
        r.raise_for_status()
        print(r.json())
    except:
        pass
## Additional Example Response
**GET** http://proxy.exposed/?ip=22.33.44.55

    {
      "proxy": "transparent",
      "headers": {
        "Host": "proxy.exposed",
        "Connection": "close",
        "User-Agent": "python-requests/2.28.1",
        "Accept-Encoding": "gzip, deflate, br",
        "Accept": "*/*"
      },
      "proxy_headers": {
        "X-IP": "22.33.44.55",
        "X-Country": "US"
      },
      "requesting_ip_address": "1.2.3.4",
      "real_ip_leak": true
    }
## Proxy Definitions

### Elite
The target server does not know that the client is using a proxy, and the client's IP address is not visible.
### Anonymous
The target server sees that the client is using a proxy, but does not see the client's IP address.
### Transparent
The client's origin IP address is visible to the target server.

## To know

 - Use without any limits (😌😬).
   
 - If you get redirected back here, or this page is returned to you from
   a request, it likely means you did not include the `ip` parameter in
   your request.
   
 - It should go without saying, but I'll say it just in case, no, your
   real ip address is not saved, neither shared with anyone.

Any comments, problems, questions, tweet me — [@_stayml](https://twitter.com/_stayml)
 

