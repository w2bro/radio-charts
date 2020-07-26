# 📡 direwolf
This is a helm chart for deploying the [`w2bro/direwolf`] docker image

## Quick Start
```shell
helm repo add w2bro https://radio-charts.w2bro.dev
helm install w2bro/direwolf
```

## Installing the Chart
To install the chart with the release name `aprs-igate`:

```shell
helm install --name aprs-igate w2bro/direwolf
```

**IMPORTANT NOTE:** a RTL-SDR USB dongle or USB sound card must be used to interface with a reiver and optional transmitter in order for this chart to function properly.

A way to achieve this can be with `nodeSelector` and specifying that node, or `nodeAffinity` rules to find a node with the label `app: aprs-igate`:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: app
          operator: In
          values:
          - aprs-igate
```

## Uninstalling the Chart
```shell
helm delete aprs-igate --purge
```

## Configuration
Review the repo's default configuration in the [values.yaml] file.

Create your own YAML configuration file and specify your own environment variables. Be sure to set the callsign with your SSID (ex: `W2BRO-10` for igate) & the required [IGLOGIN passcode].
Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```shell
helm install --name aprs-igate -f callsign-values.yaml w2bro/direwolf
```

[`w2bro/direwolf`]: https://github.com/w2bro/docker-direwolf
[values.yaml]: https://github.com/w2bro/radio-charts/blob/master/charts/direwolf/values.yaml
[IGLOGIN passcode]: http://apps.magicbug.co.uk/passcode/
