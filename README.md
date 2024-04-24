# flutter_get_serial

```
  String serial = "-";

  Future<void> getSerialNumber() async {
    debugPrint("getSerialNumber");
    try {
      final result = await Process.run('sh', [
        '-c',
        "ifconfig | grep wlan0 | grep -o -E '([[:xdigit:]]{1,2}:){5}[[:xdigit:]]{1,2}'"
      ]);

      if (result.exitCode == 0) {
        setState(() {
          serial = result.stdout.trim().replaceAll(":", "");
        });
      } else {
        setState(() {
          serial = 'Failed to get serial number: ${result.stderr}';
        });
      }
    } catch (e) {
      setState(() {
        serial = 'Error getting serial number: $e';
      });
    }
  }
```
