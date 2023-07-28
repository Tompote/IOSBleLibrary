# BleLib

A BluetoothLE library for iOS

## Usage

### Initialization

Create an instance of DeviceManager. There should be only one instance inside your project.

```swift
private var deviceManager: DeviceManager?
```

then call

```swift
self.deviceManager = DeviceManager(self.viewController, self.displayStrings, {(success, message) -> Void in
            if success {
                // Code to run on success
            } else {
                // Code to run on failure
            }
        })
```
Note:\
self.viewController: Your current UIViewController\
self.displayStrings: The messages you want to display

```
displayStrings["noDeviceFound"] = "No device found"
displayStrings["availableDevices"] = "Available devices"
displayStrings["scanning"] = "Scanning..."
displayStrings["cancel"] = "Cancel"
```

### Scanning

DeviceManager exposes a startScanning function that returns devices inside the ScanResultCallback

```swift
public func startScanning(
        _ serviceUUIDs: [CBUUID],
        _ name: String?,
        _ namePrefix: String?,
        _ allowDuplicates: Bool,
        _ shouldShowDeviceList: Bool,
        _ scanDuration: Double?,
        _ callback: @escaping Callback,
        _ scanResultCallback: @escaping ScanResultCallback
    )
```
You can use the stopScan() function to stop scanning

### Connect

DeviceManager exposes a connect function that allows to connect to a specific device

```swift
public func connect(
        _ device: Device,
        _ connectionTimeout: Double,
        _ callback: @escaping Callback
    )
```

### Disconnect

DeviceManager exposes a connect function that allows to disconnect from a specific device

```swift
public func disconnect(
        _ device: Device,
        _ timeout: Double,
        _ callback: @escaping Callback
    )
```

### Read

To read a value from a specific service and characteristic you can use the Device.read function:

```swift
public func read(
        _ serviceUUID: CBUUID,
        _ characteristicUUID: CBUUID,
        _ timeout: Double,
        _ callback: @escaping Callback
    )
```

### Write

To write a value to a specific service and characteristic you can use the Device.write function:

```swift
public func write(
        _ serviceUUID: CBUUID,
        _ characteristicUUID: CBUUID,
        _ value: String,
        _ writeType: CBCharacteristicWriteType,
        _ timeout: Double,
        _ callback: @escaping Callback
    )
```

### Notifications

To start/stop listening for notifications on a specific service and characteristic you can use the Device.setNotifications function:

```swift
public func setNotifications(
        _ serviceUUID: CBUUID,
        _ characteristicUUID: CBUUID,
        _ enable: Bool,
        _ notifyCallback: Callback?,
        _ timeout: Double,
        _ callback: @escaping Callback
    )
```

### RSSI

To know the connection quality you can use Device.readRssi:

```swift
public func readRssi(
        _ timeout: Double,
        _ callback: @escaping Callback
    )
```
