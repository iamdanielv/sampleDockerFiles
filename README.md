# sampleDockerFiles
Sample docker files showing good practices

## Check Rate limit
Docker limits the number of container pulls per IP address, in order to see how many you have used you can run the following:

``` shell
export TOKEN=$(curl "https://auth.docker.io/token?service=registry.docker.io&scope=repository:ratelimitpreview/test:pull" | jq -r .token)
curl --head -H "Authorization: Bearer $TOKEN" https://registry-1.docker.io/v2/ratelimitpreview/test/manifests/latest
```
> Note: You will need to have **curl** and **jq** installed for the above command to work

it should return something similar to:

``` shell
ratelimit-limit: 100;w=21600
ratelimit-remaining: 100;w=21600
```
