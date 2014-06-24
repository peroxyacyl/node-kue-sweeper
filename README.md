# kue-sweeper
a simple nodejs service to avoid memory leaking when use kue to process millions of jobs by removing kue job immediately upon its completion

## Why need this module:
[kue](https://npmjs.org/package/kue) is a handy redis-backed job processing module. But when using kue for processing millions of jobs, we have met following circumstances incuring memory leaking.

 * [job related search sets remain in redis after job got removed](https://github.com/learnboost/kue/issues/94)
 * Job handling service crash causes job pilling in redis

So I wrote this little tool to run as a standalone service (**via forever**) which will keep watching kue and remove kue job immediately upon its completion

## Install

Install [forever tool](https://npmjs.org/package/forever)
```bash
npm install forever -g
```

Install the kue-sweeper
```bash
npm install kue-sweeper
```

## Usage

```bash
# start kue-sweeper with forever
./forever-start-kue-sweep.sh
```


## Configure

 * -p --port <n> or config.redis.port, redis service port
 * -h, --host [VALUE] or config.redis.host, redis service host

## License
Copyright (c) 2013 yi
Licensed under the MIT license.
