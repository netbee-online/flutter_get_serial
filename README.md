# flutter_get_serial

```
  String serial = "-";

  Future<void> getSerialNumber() async {
    debugPrint("getSerialNumber");
    try {
      final result = await Process.run('sh', [
        '-c',
        'getprop | grep -i ro.serialno | cut -d \']\' -f 2 | cut -d \'[\' -f 2'
      ]);

      if (result.exitCode == 0) {
        setState(() {
          serial = result.stdout.trim();
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
