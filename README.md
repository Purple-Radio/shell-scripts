# Shell Scripts

Collection of short shell scripts that run on our radio backend and automate processes. Scripts should be applicable to most installations running libretime unless indicated otherwise. Most scripts will require that the API is enabled within libretime settings.

## Script Functions

| Script         | Function                                                     |
| -------------- | ------------------------------------------------------------ |
| record_shows   | Infinite loop that uses ffmpeg to record the icecast stream output during show blocks. An array of ignored show block titles can be defined (minus whitespace) to skip automated segments. The script uses libretimes API to sleep until the beginning of the next show block and limit system load, beware of edge case where script is sleeping and misses a last minute change to the schedule, best to change shows at least an hour in advance. |
| clear_messages | Infinite loop that queries the schedule API and sleeps till the next scheduled show start before clearing DJ messages. The script uses libretimes API to sleep until the beginning of the next show block and limit system load, beware of edge case where script is sleeping and misses a last minute change to the schedule, best to change shows at least an hour in advance. |

## Installation

- Copy the script you want to install directly to a folder in the path.

> The systemd units provided assume the scripts are present in /usr/bin, if you want to use a different directory be sure to modify the systemd unit accordingly.

```bash
cp /scripts/foo /usr/bin/.
```

- Make the script executable:

```shell
chmod +x foo
```

- If you want the script to run at boot, copy the corresponding systemd service and enable it

```bash
cp /services/foo.service /etc/systemd/system/
systemctl start foo.service
systemctl enable foo.service
```

