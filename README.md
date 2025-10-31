COZIR CO2 Sensor Data Logger (ESP8266 + InfluxDB)
A robust Arduino sketch designed to read CO2 concentration data from a COZIR non-dispersive infrared (NDIR) sensor and wirelessly transmit it to an InfluxDB Time-Series Database using an ESP8266 microcontroller.

1. Features
COZIR Sensor Integration: Communicates with the COZIR sensor via SoftwareSerial for accurate CO2 readings in ppm (parts per million).
InfluxDB Logging: Efficiently pushes time-stamped sensor data directly to a specified InfluxDB bucket.
WiFi Connectivity: Utilizes the ESP8266's built-in WiFi to establish a stable connection.
Configurable: Easy setup via #define directives for WiFi credentials, InfluxDB server details (URL, Token, Org, Bucket), and debug output.
Robustness: Includes basic sanity checks for CO2 readings and automatic WiFi reconnection logic.

2. Implementation Details
The core functionality for reading the CO2 sensor is based on the manufacturer's provided example code, which handles the specific serial protocol (Q\r\n command and parsing).This sketch adapts that fundamental sensor reading logic by:

- Refactoring the code for enhanced readability and robustness.
- Integrating the reading process with the ESP8266's WiFi capabilities.
- Adding the necessary client setup and transmission logic for sending data points to a remote InfluxDB database.

This approach ensures the highest compatibility with the COZIR sensor while providing a modern, cloud-logging solution.

3. Hardware Requirements
Microcontroller: ESP8266 board (e.g., NodeMCU, Wemos D1 Mini).
CO2 Sensor: COZIR NDIR Sensor.
Cables/Breadboard: For wiring the components.

4. Configuration
Before uploading the sketch, you must update the following #define settings in the main .ino file:

	WiFi & InfluxDB Credentials
	Replace the placeholder values with your actual network and database information:
	
	// --- WiFi Configuration  ---
	#define WIFI_SSID "WIFI_SSID" 
	#define WIFI_PASS "WIFI_PSW" 
	
	// --- InfluxDB Configuration  ---
	#define INFLUXDB_URL "http://xxx.xxx.xxx.xxx:8086" 		// Influx Database IP address and port
	#define INFLUXDB_TOKEN "INFLUX_TOKEN"             		// InfluxDB API token
	#define INFLUXDB_ORG "xxx"                       	  	// Influx Organization name
	#define INFLUXDB_BUCKET "xxx"              				// Influx bucket name
	Operational Modes
	You can enable or disable key functionalities using these flags:
	#define DEBUG		Enables detailed output to the Serial Monitor (recommended for testing).
	#define WIFI		Enables WiFi connection and InfluxDB data transmission. Disable to test sensor reading only.

5. Getting Started
Install Libraries: Ensure you have the following libraries installed in your Arduino IDE:
	- SoftwareSerial (Usually built-in)
	- ESP8266WiFi (Built-in with ESP8266 board support)
	- InfluxDbClient (Available via the Library Manager)
Configure: Update the credentials in the sketch as described above.
Upload: Select the correct board and port, and upload the sketch to your ESP8266.
Monitor: Open the Serial Monitor (set to 9600 baud) to track connection status and data readings (if DEBUG is enabled).
