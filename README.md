- sendPlayerCount.lua README

## Overview

The `sendPlayerCount.lua` script is designed for Multi Theft Auto (MTA) servers to periodically send server information, including the server name, player count, IP address, and online status, to a specified API endpoint. The script uses HTTP POST requests to transmit data in JSON format.

## Functionality

- **Data Collection**: Collects the server name, current player count, server IP, and a static "Online" status.
- **Data Transmission**: Sends the collected data as a JSON payload to the API endpoint `https://example.app/api/app`.
- **Periodic Execution**: Uses a timer to execute the data-sending function every 60 seconds.
- **Callback Handling**: Includes a placeholder callback function to handle the API response or errors.

## Requirements

- **Multi Theft Auto (MTA)**: The script is designed to run on an MTA server.
- **Lua Environment**: Requires MTA's Lua functions (`getServerName`, `getPlayerCount`, `getServerConfigSetting`, `toJSON`, `fetchRemote`, `setTimer`).
- **Network Access**: The server must have internet access to send HTTP POST requests to the specified API endpoint.

## Installation

1. Place the `sendPlayerCount.lua` file in your MTA server's resource directory (e.g., `mods/deathmatch/resources/[your_resource]/`).

2. Add the script to your resource's `meta.xml` file:

   ```xml
   <script src="sendPlayerCount.lua" type="server" />
   ```

3. Start or restart the resource using the MTA server console (`/start [resource_name]` or `/refresh`).

## Usage

- The script automatically starts sending data to the API upon resource start.
- Data is sent every 60 seconds (60000 milliseconds) in an infinite loop (`setTimer` with `0` iterations).
- The API endpoint (`http://localhost/api/app`) must be accessible and configured to accept POST requests with JSON data.

## Script Details

- **Function** `enviarDadosServidor`:
  - Collects server data (name, player count, IP, and status).
  - Converts data to JSON format using `toJSON`.
  - Removes the JSON array brackets (`string.sub(tbl, 2, -2)`) to match the expected API format.
  - Sends the data via `fetchRemote` with `Content-Type: application/json`.
- **Function** `callBack`:
  - A placeholder function to handle the API response or errors (currently empty).
- **Timer**: Executes `enviarDadosServidor` every 60 seconds and runs immediately on resource start.

## Customization

- **API Endpoint**: Modify the `url` variable to point to a different API endpoint if needed.
- **Timer Interval**: Adjust the `60000` in `setTimer` to change the frequency of data transmission (in milliseconds).
- **Data Fields**: Add or modify fields in the JSON table within `enviarDadosServidor` to suit your API requirements.
- **Callback Logic**: Implement logic in the `callBack` function to handle API responses or errors (e.g., logging, error handling).

## Notes

- Ensure the API endpoint supports the JSON format sent by the script (without array brackets).
- The script assumes the `fetchRemote` function is available in the MTA environment.
- Test the script in a development environment to verify API compatibility and handle potential network issues.

## Troubleshooting

- **API Errors**: Check the `callBack` function for error codes or messages returned by the API.
- **Network Issues**: Verify that the MTA server can reach the API endpoint (`http://localhost/api/app`).
- **JSON Format**: Ensure the API accepts the JSON structure sent by the script.
