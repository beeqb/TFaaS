#### Python client
For Python client example we'll use
[tfaas_client.py](https://github.com/vkuznet/TFaaS/blob/master/src/python/tfaas_client.py).
Similar to 
[Curl](https://github.com/vkuznet/TFaas/blob/master/doc/curl_client.md) 
client use case we need to upload our model to TFaaS server.
This can be done by creating *upload.json* file with our upload parameters:
```
{
  "model": "/path/tf_model.pb", "labels": "/path/labels.txt",
  "name": "myModel", "params":"/path/params.json"
}
```
It includes full path to our TF model, labels and parameters files as well as
name of our TF model. Now we can run our python client:
```
# define url for TFaaS
url=http://localhost:8083

# upload our model
tfaas_client.py --url=$url --upload=upload.json

# view registered models in TFaaS server
tfaas_client.py --url=$url --models
```
Finally, we can ask for predictions by preparing *input.json* file which
contains our keys (the list of names of our parameters), their values (the list
of numerical values) and model name we want to use for inference, e.g.:
```
{"keys":["attr1", "attr2", ...], "values":[1,2,...], "name":"myModel"}
```
We can place the following call to get our predictions:
```
tfaas_client.py --url=$url --predict=input.json
```

When we deal with images, i.e. perform image classification, we use the
following API:
```
# send request to classify given image (in this case we uploaded HEP_images model)
tfaas_client.py --url=$url --image=/path/file.png --model=HEP_images
# the server response will looks like this (here the labels contains
# three classes: higgs, qcd and muons)
{"filename":"/path/file.png","labels":[{"label":"higgs","probability":1},{"label":"qcd","probability":2.815438e-8},{"label":"muons","probability":4.65911e-18}]}
```
