# fluentstream

> fluentstream test

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

```

Question: Do I have to actually npm install and run this whole dev sever thing?
Answer: Yes probably, it proxies the API requests.  You can disable chrome security and change the urls on the requests if you want.

Question: What tools did you use to make this?
Answer: Webpack config and project structure c/o Vue cli. There is some other random junk in there too that could be removed (font awesome, lodash).  I wanted to try out some new libraries so I used axios for http requests just because it seems very popular recently, and vue-bootstrap, which seemed to work pretty good, but was way more verbose than I cared for.

Tested with node 6.9.2 & Chrome