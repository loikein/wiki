# Homebridge

## Config

```json
{
    "bridge": {
        "name": "Homebridge ACD5",
        "username": "0E:23:65:0E:AC:D5",
        "port": 51157,
        "pin": "383-68-664"
    },
    "accessories": [
       {
            "accessory": "SwitchBot-For-Mac",
            "name": "Switch",
            "delay": 5000,
            "retries": 3,
            "macAddress": "F6:9B:56:E3:2A:F3",
       }
    ],
    "platforms": [
        {
            "name": "Config",
            "port": 8581,
            "platform": "config"
        }
    ]
}
```

## How to

- Restart: `$ sudo systemctl restart homebridge`

