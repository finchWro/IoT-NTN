# IoT-NTN Script

This project provides a script for IoT devices supporting LTE-M with NB-IoT NTN fallback. The script automates modem initialization, network selection, GNSS location acquisition, and UDP data transmission.

## Features

- LTE-M and NB-IoT NTN access selection
- Automatic fallback between LTE-M and NB-IoT NTN
- GNSS location acquisition and reporting
- UDP data transmission to configurable server
- Band and APN configuration

## Configuration

Edit `client.ttl` to set parameters:

- `timeout`: Response wait time (seconds)
- `dataloop`: Interval between data sends (seconds)
- `LTEMBand`, `NTNBand`: Band configuration for LTE-M and NTN
- `primaryAccess`: Set to `0` for LTE-M primary, `1` for NB-IoT NTN primary
- `APN`, `udpServer`, `udpPort`: Network and server settings

## Operation

1. **Initialization**: Modem is reset and configured for multi-RAT and GNSS.
2. **Access Selection**: Device selects LTE-M or NB-IoT NTN based on `primaryAccess`.
3. **Network Attach**: Device attaches to the selected network and configures band and APN.
4. **GNSS Fix**: Device attempts to acquire GNSS location.
5. **Data Transmission**: Location and radio measurements are sent as UDP packets to the configured server.
6. **Fallback**: If network or GNSS acquisition fails, the script automatically falls back to the alternate access technology.

## Data Format

Data is sent as a JSON object containing:

- `lat`, `lng`: GNSS coordinates
- `type`: Access technology (`LTEM` or `NB-IoT-NTN`)
- `RSRP`, `RSRQ`, `SINR`, `RSSI`: Radio measurements

The JSON is converted to HEX before transmission.

## Usage

Upload `client.ttl` to your IoT device and ensure modem supports required AT commands.

Modify configuration parameters as needed for your deployment.

