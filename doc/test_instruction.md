# General Testing Step

## yarn run watch

First, open a terminal and cd into the root directory of MassBrowser:
```sh
cd MassBrowser
```

Only for the first time, we need to install all the dependencies:
```sh
yarn
```

Then start the auto-compilation program:
```sh
yarn run watch
```
Note that we can leave this terminal open and this program running so that whenver there is any changes to the source code, it will help you compile it on the fly!

## Run MassBrowser

### CLI

``` sh
yarn run relay:dev
yarn run client:dev
```

### GUI

``` sh
yarn run dev:relay
yarn run dev:client
```

## Helpful testing website

MassBrowser uses different censorship circumvention strategies based on the websites user would like to access. To do the testing, first run the MassBrowser and then try to open a website via curl or Firefox. The output and degbugging information can be seen from the console.

### Vanilla Proxy

Vanilla proxy is actually letting client connect to the website directly.

`www.baidu.com` is under vanilla proxy policy and is uncensored.

Apart from using MassBrowser to test it, we can also use curl from commandline:

```sh
curl -x socks5h://localhost:7080 https://www.baidu.com
```

The output from MassBrowser should be similar to:

    debug: New socks connection to www.baidu.com:443 using policy 'vanilla_proxy'

### CacheBrowsing

`cnn.com` is accessible with CacheBrowsing.

Apart from using MassBrowser to test it, we can also use curl from commandline:

```sh
curl -x socks5h://localhost:7080 https://cdn.cnn.com
```

The output from curl should be similar to:

	curl: (60) SSL certificate problem: unable to get local issuer certificate
	More details here: https://curl.haxx.se/docs/sslcerts.html

	curl failed to verify the legitimacy of the server and therefore could not
	establish a secure connection to it. To learn more about this situation and
	how to fix it, please visit the web page mentioned above.

This is because curl is not using the local CA installed by MassBrowser. The cachebrowsable webistes should still be accessible via Firefox.

The output from MassBrowser should be similar to:

    debug: New socks connection to cdn.cnn.com:443 using policy 'cachebrowse'

### Mass Buddies

`www.youtube.com` is accessible with the help of Mass Buddies, which are also known as yaler proxies.

Apart from using MassBrowser to test it, we can also use curl from command line:

```sh
curl -x socks5h://localhost:7080 https://www.youtube.com
```

The output from MassBrowser should be similar to:

    debug: New socks connection to www.youtube.com:443 using policy 'yaler_proxy'
    debug: Assigning session for www.youtube.com of category Video Streaming
    debug: Searching sessions for Video Streaming
    debug: Sessions for Video Streaming Assigned
    debug: Relay [VAJKfsSLK] assigned for connection
