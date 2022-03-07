---
layout: post
---
<!-- # QRcode Generator Documentation -->
API version: `1.0`
## Introduction
QRcodesvc is a powerful QRcode generator that can be used to generate high-quality QR codes for any use case. It is supports all major formats: PNG, PDF, EPS, and SVG. With just one endpoint, you can create a QR code with your desired format, design & size in seconds.

<!-- 
## API Limitation
None -->

### Price
Newbapi offers three tiers of service: Basic, Pro, and Ultra.

|                          | Basic         | Pro         | Ultra            |
| ------------------------ | ------------- | ----------- | -----------------|
| Request                  | 1K / Month    | 24M / Month | $0.00000101 / use|
| Rate Limit (Per second)  | 1             | 10          | 10               |
| Price                    | Free          | $24.00      | Pay Per Use      |


Subscribe Here: [RapidAPI](https://rapidapi.com/newbAPIOfficial/api/qrcodesvc-qrcode-generator/pricing)

## Endpoint Info

List of available endpoint:

| Endpoint            	   | Method  | 
| ------------------------ | --------| 
| `api/v1/qrcodesvc/text`  | `POST`  | 


## API request body


| Parameter / Query | Type         | Default | Description      | Example
| ----------------- | ------------ | --------| ---------------- | ---------------------------
| data              | `string`     | `none`  | Qr code data     | `https:\\jaironlanda.com` or `this is normal text`


### Request body `config`

| Parameter / Query | Type         | Default | Description      | Example
| ----------------- | ------------ | --------| ---------------- | ----------
| auto              | `boolean`     | `true`  | Generate qr code with default config. Default Config: `"version": 1`, `"error_correction": "M"`, `"box_size": 10`, `"border": 4` | -
| version    | `integer`    | `1` | Supported qr code version: `1` until `40` | -
| error_correction  | `string`     | `'M'`   | Error correction config: `L`, `M` (default), `Q`, and `H` | -
| box_size| `integer`      | `10`  | Minimum: `10`, Maximum: `100` | -
| border  | `integer`      | `4`  | Minimum: `4`| -

#### Example #1:

Generate qr code with config `"auto": true`. Parameter `version`, `error_correction`, `box_size`, and `border` is not require.
```
{
    "data": "jaironlanda.com",
    "config": {
        "auto": true
    },
    "option": {
        "file_type": "png"
    }
}
```
> Note: `design` parameter is optional. Default color is black and white.

#### Example #2:
To generate qr code with custom config set `auto` parameter to `false`.

```
{
    "data": "jaironlanda.com",
    "config": {
        "auto": false,
        "version": 20,
        "error_correction": "L",
        "box_size": 50,
        "border": 10
    },
    "option": {
        "file_type": "png"
    }
}
```
> Note: `design` parameter is optional. Default color is black and white.

### Request body `design`

> Note: Support color format `Hex color` only. More info [here](https://www.color-hex.com/)

| Parameter / Query | Type         | Default | Description      | Example
| ----------------- | ------------ | --------| ---------------- | ----------
| qr_colour         | `string`     | `#000000`  | Qr code color, default is black color or `#000000` | -
| bg_colour    		| `string`    | `#ffffff` | Background for qr code, default is white color or `#ffffff` | -

#### Example #3:
Generate qr code with custom color and auto config.
```
{
    "data": "jaironlanda.com",
    "config": {
        "auto": true
    },
    "design": {
        "qr_colour": "#f69273",
        "bg_colour": "#cc0000"
    },
    "option": {
        "file_type": "png"
    }
}
```
#### Example #4:
Generate qr code with custom color and manual config.
```
{
    "data": "jaironlanda.com",
    "config": {
       "auto": false,
        "version": 20,
        "error_correction": "L",
        "box_size": 50,
        "border": 10
    },
    "design": {
        "qr_colour": "#f69273",
        "bg_colour": "#cc0000"
    },
    "option": {
        "file_type": "png"
    }
}
```

### Request body `option`

| Parameter / Query | Type         | Default | Description      | Example
| ----------------- | ------------ | --------| ---------------- | ----------
| file_type              | `string`     | `png`  | support file type: `png`, `pdf`, `eps`, and `svg`| -
| file_name    | `string`    | `none` | if value is none, file name will randomly generate | -

#### Example #5:
Generate qr code with `pdf` format. Supported file type: `png`, `pdf`, `eps`, and `svg`
```
{
    "data": "jaironlanda.com",
    "config": {
        "auto": true
    },
    "option": {
        "file_type": "pdf"
    }
}
```

#### Example #5:
Generate qr code with `pdf` file type and manual config setup.
```
{
    "data": "jaironlanda.com",
    "config": {
        "auto": false,
		"version": 20,
        "error_correction": "L",
        "box_size": 50,
        "border": 10
    },
    "design": {
        "qr_colour": "#f69273",
        "bg_colour": "#cc0000"
    },
    "option": {
        "file_type": "pdf",
		"file_name": "this is my qrcode"
    }
}
```

### Schema

Schema for API request: 
```
{
	"title": "QrText",
	"required": [
		"config",
		"option"
	],
	"type": "object",
	"properties": {
		"data": {
			"title": "Data",
			"type": "string",
			"default": "jaironlanda.com"
		},
		"config": {
			"title": "QrConfig",
			"type": "object",
			"properties": {
				"auto": {
					"title": "Auto",
					"type": "boolean",
					"default": true
				},
				"version": {
					"title": "Version",
					"type": "integer",
					"default": 1
				},
				"error_correction": {
					"title": "Error Correction",
					"type": "string",
					"default": "M"
				},
				"box_size": {
					"title": "QR code Box Size minium is 10",
					"maximum": 100,
					"minimum": 10,
					"type": "integer",
					"default": 30
				},
				"border": {
					"title": "Border",
					"type": "integer",
					"default": 4
				}
			}
		},
		"design": {
			"title": "QrDesign",
			"type": "object",
			"properties": {
				"qr_colour": {
					"title": "Qr Colour",
					"type": "string",
					"default": "#000000"
				},
				"bg_colour": {
					"title": "Bg Colour",
					"type": "string",
					"default": "#ffffff"
				}
			}
		},
		"option": {
			"title": "QrOption",
			"type": "object",
			"properties": {
				"file_type": {
					"title": "File Type",
					"type": "string",
					"default": "png"
				},
				"file_name": {
					"title": "File Name",
					"type": "string"
				}
			}
		}
	}
}
```
## API response

```
....
"content-disposition":"attachment; filename*=utf-8''<file-name-here>.<file-format>"
"content-type":"<content type>"
....
```

List of `content-type`:
- PDF: `application/pdf`
- EPS: `application/postscript`
- PNG:  `image/png`
- SVG: `image/svg+xml`