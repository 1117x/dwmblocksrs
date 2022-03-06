dwm statusbar heavily inspired by [dwmblocks](https://github.com/torrinfail/dwmblocks).

## Features:
- Segments of statusbar can have individual update intervals
- Segments can be manually updated by sending a signal
- can be configured with config file

## Example config:
```yaml
# default separator that all segments use
left_separator: "  "
# scripts are expected to be in this folder
script_dir: "/home/example/.segments"

# signal that updates all the segments at once
update_all_signal: 0

# check every 5 times if any segment is due
# updates per signal are always instantly
general_update_interval: 5
# if this is not given, the interval will be calculated based on the individual segments

segments:
      # scripts are run with sh
    - script: "volume"
      # this segments updates once per minute
      update_interval: 60
      # or when the signal SIGRTMIN+1 comes
      # bind `pkill -RTMIN+1 dwmblocksrs` to your volume shortcuts
      signals: [1]

    - script: "battery"
      update_interval: 10
      # this segment is hidden when the script returns an empty string
      hide_if_empty: true

    - program: "date"
      args: ["+%a. %d. %B %Y"]
      update_interval: 60
      # icons are displayed to the left of the output
      icon: "  "

    - program: "date"
      args: ["+%H:%M"]
      update_interval: 60
      icon: " "
      # the default left separator gets overwritten
      left_separator: " "
```

The above config file produces the following statusbar in dwm:
```
 墳 49%    So. 06. März 2022  16:13
```
(the battery segment is hidden because the script outputs an empty string)