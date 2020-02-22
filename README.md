## provision-example

Provision a cloud host and optionally install some packages using user-data.

What's this for? This is an example of how to use the provision package as used in [inletsctl](https://github.com/inlets/inletsctl) and the [inlets-operator](https://github.com/inlets/inlets-operator)

## Tutorial

Clone/build:

```
git clone https://github.com/inlets/provision-example
cd provision-example
go build
```

Create a file `./cloud-config.txt`

```sh
#cloud-config
packages:
  - nginx
runcmd:
  - systemctl enable nginx
  - systemctl start nginx
```

Run the example:

```sh
./provision-example \
  --access-token $(cat ~/Downloads/do-access-token) \
  --userdata-file cloud-config.txt

2020/02/22 11:01:58 Provisioning host with DigitalOcean
Host ID: 181660892
Polling status: 1/250
Polling status: 2/250
Polling status: 3/250
Polling status: 4/250
Polling status: 5/250
Polling status: 6/250
Polling status: 7/250
Polling status: 8/250
Polling status: 9/250
Polling status: 10/250
Polling status: 11/250
Your IP address is: 64.227.34.235
```

Then try the host:

```
curl -s 64.227.34.235 | head -n 4
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
```

Delete any hosts you create via your dashboard, or using the cloud-provider's CLI.

## Contributing

Please follow the [inlets contributing guide](https://github.com/inlets/inlets/blob/master/CONTRIBUTING.md)

Need support? Join the [OpenFaaS Slack and the #inlets channel](https://slack.openfaas.io/), or open an issue if there is a genuine issue with the code.