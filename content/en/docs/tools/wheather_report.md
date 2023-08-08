---
title: "Wheather Report"
description: "Create a weather report for your location... Ekhm, I mean financial report in form of charts."
lead: "Create a ☔️ weather report for your location... Ekhm, I mean 💸 financial report in form of 📈 charts."
date: 2023-08-09T00:45:48+02:00
lastmod: 2023-08-09T00:45:48+02:00
draft: false
images: []
menu:
  docs:
    parent: ""
    identifier: "wheather_report-e10043cfd16f76798b1419df06e21e41"
weight: 999
toc: true
---

<img src="https://img.shields.io/badge/license-MIT-violet.svg" alt="MIT License">

You can generate charts for your choose of currency and time period of 1 day
or 1 hour using [Oanda](https://www.oanda.com/) API.

You can generate charts for your choose of stock and time period of 1 day
or 1 hour using [Finnhub](https://finnhub.io) API.

You can generate charts for your choose of stock and time period of 1 day
using [Yahoo Finance](https://finance.yahoo.com/) API.

## Installation

Clone, or copy the repository and install the requirements.

```shell
# for virtualenv
pip install -r requirements.txt
# for python3
python3 -m pip install -r requirements.txt
```

Register for [Oanda](https://www.oanda.com/) API and get your API key. You can use demo (practice) account.

Register for [Finnhub](https://finnhub.io) API and get your API key. US stocks are free to use.

Yahoo Finance API is free to use.

Repository is available on [GitHub](https://github.com/nutek-terminal/wheather_report)

## Usage

Create chart for CHF/JPY currency pair for 1 day and 1 hour with about few
months of data.

```shell
python3 weather_report.py --token <your_oanda_token> --account <your_account_id> --instruments CHF_JPY
```

Display help message.

```shell
python3 weather_report.py --help
```

Display daily chart of AAPL stock for 1 day with few months of data.

```shell
python3 wheater_report.py --yahoo AAPL
```

## What's displayed on the chart?

Chart #1

- Ichimoku Cloud
- CCI
- Volume
- Price line chart

Chart #2

- RSI
- MACD
- Volume
- Price line chart

## Link to the repository

Get more information about Wheather Report on [GitHub](https://github.com/nutek-terminal/wheather_report)