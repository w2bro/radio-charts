# 📡 readsb
This is a helm chart for deploying the [`mikenye/readsb`] docker image

## Quick Start
```shell
helm repo add w2bro https://radio-charts.w2bro.dev
helm install w2bro/readsb
```

## Installing the Chart
To install the chart with the release name `readsb-release`:

```shell
helm install --name readsb-release w2bro/readsb
```

**IMPORTANT NOTE:** a USB RTL SDR dongle must be used, I am using the blue FlightAware stick connected to a FlightAware ADS-B antenna.

A way to achieve this can be with `nodeSelector` and specifying that node, or `nodeAffinity` rules to find a node with the label `usb-device: adsb-antenna`:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: usb-device
          operator: In
          values:
          - adsb-antenna
```

## Uninstalling the Chart
```shell
helm delete readsb-release --purge
```

## Configuration
Review the repo's default configuration in the [values.yaml] file.

Create your own YAML configuration file and specify your own environment variables. Be sure to set the callsign with your SSID (ex: `W2BRO-10` for igate) & the required [IGLOGIN passcode].
Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```shell
helm install --name aprs-igate -f callsign-values.yaml w2bro/direwolf
```

[`mikenye/readsb`]: https://github.com/mikenye/docker-readsb
[values.yaml]: https://github.com/w2bro/radio-charts/blob/master/charts/readsb/values.yaml
