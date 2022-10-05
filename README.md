# grafana-cs
Grafana snap with content interface

## Description
Grafana snap which provides a content interface slot called "writable".
The "writable" slot allows r/w on $SNAP_DATA/conf. Tipical usage is to add/modify a custom grafana.ini file.

To connect to the interface, your snap should declare a "writable" slot as described below:
```
plugs:
   writable:
     interface: content
     content: writable-data
     target: <your target dir>
```
More info on content interface here: https://snapcraft.io/docs/content-interface

## How to use it
Use the following command to connect the interface:
```
snap connect <your-snap-name>:writable grafana-cs:writable
```

# Grafana plugins
To include Grafana plugin, add the following to snapcraft.yaml

```
<plugin_id>:
    plugin: dump
    source: <link to zip file of the plugin
    source-type: zip
```
Then configure the install hook to copy the plugin in the grafana plugin directory:
```
cp -r ${SNAP}/<plugin id> ${SNAP_COMMON}/data/plugins
```

