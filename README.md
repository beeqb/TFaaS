### TensorFlow as a Service (TFaaS)

[![Build Status](https://travis-ci.org/vkuznet/TFaaS.svg?branch=master)](https://travis-ci.org/vkuznet/TFaaS)
[![Go Report Card](https://goreportcard.com/badge/github.com/vkuznet/TFaaS)](https://goreportcard.com/report/github.com/vkuznet/TFaaS)
[![License:MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/vkuznet/LICENSE)
[![DOI](https://zenodo.org/badge/109141847.svg)](https://zenodo.org/badge/latestdoi/109141847)
[![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=TensorFlow%20as%20a%20service%20&url=https://github.com/vkuznet/TFaaS&hashtags=tensorflow,go,python)

A general purpose framework (written in Go) to serve TensorFlow models.
It provides reach and flexible set of APIs to efficiently access your
favorite TF models via HTTP interface. The TFaaS supports JSON and ProtoBuffer
data-formats.

The following set of APIs is provided:
- ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) `/upload` to push your favorite TF model to TFaaS server
- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) `/delete` to delete your TF model from TFaaS server
- ![#1589F0](https://placehold.it/15/1589F0/000000?text=+) `/models` to view existing TF models on TFaaS server
- ![#521b92](https://placehold.it/15/521b92/000000?text=+) `/json` to serve TF model predictions in JSON data-format
- ![#9437ff](https://placehold.it/15/9437ff/000000?text=+) `/proto` to serve TF model predictions in ProtoBuffer data-format

### From deployment to production
#### &#10112; install docker image (TFaaS port is 8083)
```
docker run --rm -h `hostname -f` -p 8083:8083 -i -t veknet/tfaas
```

#### &#10113; upload your TF model to TFaaS server
```
curl -X POST http://localhost:8083/upload
-F 'name=ImageModel' -F 'params=@/path/params.json'
-F 'model=@/path/tf_model.pb' -F 'labels=@/path/labels.txt'
```

#### &#10114; get your predictions
```
curl https://localhost:8083/image -F 'image=@/path/file.png' -F 'model=ImageModel'
```

Fore more information please visit [curl client](https://github.com/vkuznet/TFaaS/blob/master/doc/curl_client.md) page.

### TFaaS interface
Clients communicate with TFaaS via HTTP protocol. See examples for
[Curl](https://github.com/vkuznet/TFaaS/blob/master/doc/curl_client.md),
[Python](https://github.com/vkuznet/TFaaS/blob/master/doc/python_client.md)
and
[C++](https://github.com/vkuznet/TFaaS/blob/master/doc/cpp_client.md)
clients.

### TFaaS benchmarks
Benchmark results on CentOS, 24 cores, 32GB of RAM serving DL NN with
42x128x128x128x64x64x1x1 architecture (JSON and ProtoBuffer formats show similar performance):
- 400 req/sec for 100 concurrent clients, 1000 requests in total
- 480 req/sec for 200 concurrent clients, 5000 requests in total

For more information please visit
[bencmarks](https://github.com/vkuznet/TFaaS/blob/master/doc/Benchmarks.md)
page.

### More information
- [Install instructions](https://github.com/vkuznet/TFaaS/blob/master/doc/INSTALL.md) to build TFaaS from source code
- [End-to-end example of serving TF model in Go-server](https://github.com/vkuznet/TFaaS/blob/master/doc/workflow.md)
- [Demo](https://github.com/vkuznet/TFaaS/blob/master/doc/DEMO.md)
