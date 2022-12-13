# driver-card-dispenser
In order for the driver to function properly, the option variable must be configured through the MeldCX Dashboard as follows:

## Setup Options Variable
`lintech_f39000_usbid` (required) = vid:pid

vid is the usb to serial vendor ID in decimal.
pid is the usb to serial product ID in decimal.

Example:
lintech_f39000_usbid 2352:25924‬

<div align="center" >
    <img src="./Documentation/options.jpg" />
</div>

## Commands
```sh
allowCardInFromPort()
```
```sh
forbidCardInFromPort()
```
```sh
moveCardToPortHold()
```
```sh
moveCardToPortDrop()
```
```sh
collectCardIntoCollectBin()
```
```sh
moveCardFromBin()
```
```sh
checkMachinePresentBasicStatus()
```
```sh
automaticCheckingRFcardType()
```
```sh
activateRFID()
```
```sh
deactivateRFID()
```
```sh
checkRFIDCardStatus()
```
```sh
let prm = {
    // 0x0 key A - 0x1 key B
    keyNumber: 0x0,
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1,
    // Key data
    keyData: [0xff,0xff,0xff,0xff,0xff,0xff]
}  
authenticate(prm)
```
```sh
let prm = {
    // 0x0 key A - 0x1 key B
    keyNumber: 0x0,
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1
}
authenticateFromEEProm(prm)
## Note: this command is not working
```
```sh
let prm = {
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1,
    // Key A data
    keyData: [0xff,0xff,0xff,0xff,0xff,0xff]
} 
changeSectorPassword(prm)
```
```sh
let prm = {
    // 0x0 key A - 0x1 key B
    keyNumber: 0x0,
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1,
    // Key data
    keyData: [0xff,0xff,0xff,0xff,0xff,0xff]
}  
uploadPasswordToEEProm(prm)
## Note: this command is not working
```
```sh
let prm = {
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1,
    // 0x0 ~ 0x3
    startBlock: 0x0,
    // 0x1 ~ 0x3
    numberOfBlocks: 0x1
} 
readSectorBlock(prm)
```
```sh
prm = {
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1,
    // 0x0 ~ 0x3
    startBlock: 0x0,
    // 0x1 ~ 0x3
    numberOfBlocks: 0x1,
    payload: [0x0, 0x1, 0x2, 0x3, 0x4, 0x5, 0x6, 0x7, 0x8, 0x9, 0xa, 0xb, 0xc, 0xd, 0xe, 0xf]
} 
writeSectorBlock(prm)
```
```sh
prm = {
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x5,
    // 0x0 ~ 0x3
    blockNumber: 0x1,
    // initialize Value
    payload: [0x0, 0x0, 0x0, 0x1]
} 
valueInitialization(prm)
```
```sh
prm = {
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x5,
    // 0x0 ~ 0x3
    blockNumber: 0x1
} 
readValue(prm)
## Note: this command is not working
```
```sh
prm = {
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1,
    // 0x0 ~ 0x3
    blockNumber: 0x0,
    // value to increase
    payload: [0x0, 0x0, 0x0, 0x1]
}  
increaseValue(prm)
```
```sh
prm = {
    // 1K(0x0 ~ 0xf) - 4K(0x0 ~ 0x27)
    sectorNumber: 0x1,
    // 0x0 ~ 0x3
    blockNumber: 0x0,
    // value to increase
    payload: [0x0, 0x0, 0x0, 0x1]
} 
decreaseValue(prm)
```
```sh
close()
```

## RFID Operation
1. Initialise the interface
    ```sh
    initialise()
    ```
2. Check the Dispenser status
    ```sh
    checkMachinePresentBasicStatus()
    ```    
3. Allow card from port or move card from bin to read/write position
    ```sh
    allowCardInFromPort()
    moveCardFromBin()
    ```
4. Activate RFID Antena
    ```sh
    activateRFID()
    ```
5.  Check the RFID Card Status (make sure the card type is supported Mifare 1K(S50) or 4K(S70))
    ```sh
    checkRFIDCardStatus()
    ```    
6. Authenticate using Key A or Key B
    ```sh
    authenticate()
    ```
7. Call any of the following commands:
    ```sh
    - readSectorBlock()
    - writeSectorBlock()
    - increaseValue()
    - decreaseValue()
    - readValue()
    ```
8.  Move the card from read/write position to the port
    ```sh
    - moveCardToPortHold()
    - moveCardToPortDrop()    
    ```    
8. All Other Commands Can be called by it self.
