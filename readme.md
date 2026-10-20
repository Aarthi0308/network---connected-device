# Task 03: Network-Connected IoT Device

## Project Overview
This project uses an ESP32 and a DHT22 sensor to read temperature and humidity and publish the readings to an MQTT broker over Wi-Fi.

It demonstrates how an IoT device communicates over a network and handles temporary network failures.

## Features
- Reads temperature and humidity every 5 seconds.
- Publishes sensor data using MQTT over Wi-Fi.
- Automatically retries Wi-Fi and MQTT connections.
- Buffers readings when the network is unavailable.
- Publishes buffered readings after reconnection.
- Uses `millis()` for non-blocking periodic tasks.

## Components Required
- ESP32 development board
- DHT22 temperature and humidity sensor
- Wokwi online simulator

## Technologies Used
- Arduino C++
- ESP32 Wi-Fi
- MQTT protocol
- DHT22 sensor
- Wokwi simulator

## Wiring Connections

| DHT22 Pin | ESP32 Pin |
|---|---|
| VCC | 3V3 |
| DATA | GPIO 15 |
| GND | GND |
| NC | Not connected |

## How to Run

1. Open [Wokwi](https://wokwi.com/).
2. Create a new ESP32 project.
3. Add a DHT22 sensor and connect it according to the wiring table.
4. Add the required libraries: `DHT sensor library for ESPx` and `PubSubClient`.
5. Copy the program into `sketch.ino`.
6. Start the simulation.
7. Open the Serial Monitor to view sensor readings and connection status.
8. Connect an MQTT client to `broker.hivemq.com` on port `1883`.
9. Subscribe to the MQTT topic configured in the source code to view incoming readings.

## MQTT Configuration

- **Broker:** `broker.hivemq.com`
- **Port:** `1883`
- **Topic:** `aarthi-iot/task03/temperature`

The topic can be changed in the source code to a unique topic for testing.

## Offline Handling

When Wi-Fi or MQTT is unavailable, the device stores sensor readings in a fixed-size queue in RAM.

When the connection is restored, the device attempts to publish the queued readings in order.

The queue holds up to 20 readings. If the queue becomes full, the oldest reading is discarded to make room for a new reading.

## Testing and Evidence

To verify the project:

1. Run the simulation and confirm that sensor readings appear in the Serial Monitor.
2. Subscribe to the MQTT topic and confirm that messages arrive.
3. Interrupt the network connection and verify that readings are buffered.
4. Restore the connection and check that buffered readings are published.

Add screenshots of the Serial Monitor, received MQTT messages, and wiring diagram to the repository as project evidence.

## Limitations

- Buffered readings are stored in RAM and are lost if the ESP32 restarts.
- The public MQTT broker is intended for testing and does not guarantee message delivery.
- MQTT on port 1883 is unencrypted and should not be used for sensitive data.

## Conclusion

This project demonstrates a basic network-connected IoT device with sensor monitoring, MQTT communication, automatic reconnection, and offline reading buffering.

It provides practical experience with essential IoT networking concepts using an ESP32 and a simulated sensor.
