---
layout: post
---
<!-- # Word Censor With Reporting Documentation -->
API version: `1.0`
## Introduction
The Word Censor API is a powerful tool that allows you to censor bad words and their leetspeak. It has a simple RESTful API with an easy to use interface. Simply add the word to be censored, and it will be replaced with a set of asterisks (or any Characters).


## API Limitation
Word Censor API limitations are:
- Not support language: Chinese, Korean, Japanese, etc.
- Extra characters are able to bypass the scan. Example word: shittt, fuckkk

### Price
Newbapi offers three tiers of service: Basic, Pro, and Ultra.

|                          | Basic         | Pro         | Ultra            |
| ------------------------ | ------------- | ----------- | -----------------|
| Basic Scan               | 1K / Month    | 24M / Month | $0.00000101 / use|
| Advance Scan             | 10 / Month    | 24M / Month | $0.00000101 / use|
| Custom Scan              | 10 / Month    | 24M / Month | $0.00000101 / use|
| Rate Limit (Per second)  | 1             | 10          | 10               |
| Price                    | Free          | $24.00      | Pay Per Use      |


Subscribe Here: [RapidAPI](https://rapidapi.com/newbAPIOfficial/api/word-censor-with-reporting/pricing)

## Endpoint Info

List of available endpoint:

| Endpoint            | Method  | 
| ------------------- | --------| 
| `/scan/basic/text`  | `POST`  | 
| `/scan/advance/text`| `POST`  | 
| `/scan/custom/text` | `POST`  | 

### API request body

| Parameter / Query | Type         | Default | Description      | Example
| ----------------- | ------------ | --------| ---------------- | ----------
| data              | `string`     | `none`  | Text to scan     | `this is bullshit`
| partial_censor    | `boolean`    | `false` | Text censor mode | Partial: `f**k`, Full: `****`
| character_censor  | `string`     | `'*'`   | Character that use to censor word | `#`,`$`, `&` and more
| add_word_to_censor| `array`      | `none`  | Add new wordlist into default wordlist | `['dog', 'hijau', 'babi']`
| custom_word_list  | `array`      | `none`  | Prefered wordlist, default wordlist will be ignore| `['dog', 'cyka', 'blyt']`

#### Schema

Request schema: 
```
{
	"required": [
		"data"
	],
	"type": "object",
	"properties": {
		"data": {
			"title": "Data",
			"type": "string"
		},
		"partial_censor": {
			"title": "Partial Censor",
			"type": "boolean",
			"default": false
		},
		"character_censor": {
			"title": "Character Censor",
			"type": "string",
			"default": "*"
		},
		"add_word_to_censor": {
			"title": "Add Word To Censor",
			"type": "array",
			"items": {
				
			}
		},
		"custom_word_list": {
			"title": "Custom Word List",
			"type": "array",
			"items": {
				
			}
		}
	}
}
```
### API response

> ## Note
> Reporting is only available for `Advance` and `Custom` endpoint.

| Parameter / Query | Type         | Description      |
| ----------------- | ------------ | ---------------- |
| data              | `string`     | scanned text with censored word |
| total_words       | `integer`    | Total word in `data` |
| censored_text     | `array`      | List of censored word |
| total_censored    | `integer`    | Number of censored text |
| is_safe           | `boolean`    | If text is safe, it will return `true` else `false`| 



Response schema
```
{
	"required": [
		"data",
		"reports"
	],
	"type": "object",
	"properties": {
		"data": {
			"title": "Data",
			"type": "string"
		},
		"reports": {
			"title": "Reports",
			"type": "array",
			"items": {
				"title": "ScanReporting",
				"required": [
					"total_words",
					"censored_text",
					"total_censored",
					"is_safe"
				],
				"type": "object",
				"properties": {
					"total_words": {
						"title": "Total Words",
						"type": "integer"
					},
					"censored_text": {
						"title": "Censored Text",
						"type": "array",
						"items": {
							"type": "string"
						}
					},
					"total_censored": {
						"title": "Total Censored",
						"type": "integer"
					},
					"is_safe": {
						"title": "Is Safe",
						"type": "boolean"
					}
				}
			}
		}
	}
}
```
