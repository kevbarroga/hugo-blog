---
title: "Moto Scrape - Part 1"
date: 2017-10-10
tags: ["python", "web", "scrape", "development", "motogp"]
draft: true
---

## Introduction

I've been watching MotoGP for about 10 years now, and today it still amazes me that the riders have the ability to comfortably squeeze into their racing leathers with balls the size of theirs.
It's a shame the sport is not hugely popular in the states... How often do you get to see the #1 and #2 athlete compete against one another each week?

This will be a continuing series of the process I took to scrape over 30 years of MotoGP data using python.

Today we will learn how to use the python [requests](http://docs.python-requests.org/en/master/) library and the standard [json](https://docs.python.org/3.6/library/json.html) library to fetch JSON data from an URL and parse it.

## Use Requests to get data

First of all we need to have Requests installed. Please refer to the [installation of Requests](http://docs.python-requests.org/en/master/user/install/#install) if needed.

Start by importing the Requests module: 

`>>> import requests`

Create a target_url variable:

`>>> target_url = "http://www.motogp.com/en/ajax/results/selector/2017"`

We will now try to get data! Let fetch the races scheduled for the 2017 season:

`>>> races = requests.get(target_url)`

We have saved the response in the races object. As we can see races returns:

`<Response [200]>`

A good request returns 200, a bad requests returns 4XX/5XX.


Now that we have the races object, we can get all the information we need from this object.

`>>> races.text`

Returns the content of the response:

```
'{"1":{"shortname":"QAT","title":"Grand Prix of Qatar","circuit":"Losail International Circuit","sequence":"1","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/QAT"},"2":{"shortname":"ARG","title":"Gran Premio Motul de la Rep\\u00fablica Argentina","circuit":"Termas de R\\u00edo Hondo","sequence":"2","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/ARG"},"3":{"shortname":"AME","title":"Red Bull Grand Prix of The Americas","circuit":"Circuit Of The Americas","sequence":"3","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/AME"},"4":{"shortname":"SPA","title":"Gran Premio Red Bull de Espa\\u00f1a","circuit":"Circuito de Jerez","sequence":"4","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/SPA"},"5":{"shortname":"FRA","title":"HJC Helmets Grand Prix de France","circuit":"Le Mans","sequence":"5","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/FRA"},"6":{"shortname":"ITA","title":"Gran Premio d\'Italia Oakley","circuit":"Autodromo del Mugello","sequence":"6","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/ITA"},"7":{"shortname":"CAT","title":"Gran Premi Monster Energy de Catalunya","circuit":"Circuit de Barcelona-Catalunya","sequence":"7","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/CAT"},"8":{"shortname":"NED","title":"Motul TT Assen","circuit":"TT Circuit Assen","sequence":"8","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/NED"},"9":{"shortname":"GER","title":"GoPro Motorrad Grand Prix Deutschland","circuit":"Sachsenring","sequence":"9","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/GER"},"10":{"shortname":"CZE","title":"Monster Energy Grand Prix \\u010cesk\\u00e9 republiky","circuit":"Automotodrom Brno","sequence":"10","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/CZE"},"11":{"shortname":"AUT","title":"NeroGiardini Motorrad Grand Prix von \\u00d6sterreich","circuit":"Red Bull Ring \\u2013 Spielberg","sequence":"11","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/AUT"},"12":{"shortname":"GBR","title":"Octo British Grand Prix","circuit":"Silverstone Circuit","sequence":"12","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/GBR"},"13":{"shortname":"RSM","title":"Tribul Mastercard GP S.Marino e Riviera di Rimini","circuit":"Misano World Circuit Marco Simoncelli","sequence":"13","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/RSM"},"14":{"shortname":"ARA","title":"Gran Premio Movistar de Arag\\u00f3n","circuit":"MotorLand Arag\\u00f3n","sequence":"14","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/ARA"},"15":{"shortname":"JPN","title":"Motul Grand Prix of Japan","circuit":"Twin Ring Motegi","sequence":"15","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/JPN"},"16":{"shortname":"AUS","title":"Michelin\\u00ae Australian Motorcycle Grand Prix","circuit":"Phillip Island","sequence":"16","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/AUS"},"17":{"shortname":"MAL","title":"Shell Malaysia Motorcycle Grand Prix","circuit":"Sepang International Circuit","sequence":"17","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/MAL"},"18":{"shortname":"VAL","title":"Gran Premio Motul de la Comunitat Valenciana","circuit":"Circuit Ricardo Tormo","sequence":"18","url":"\\/en\\/ajax\\/results\\/selector\\/2017\\/VAL"}}'
```

In the next section we will use the json module to translate the JSON object into something python can work with.

## Decode JSON Object

Included in the Requests module is a builtin JSON decoder. We can use it instead of the standard json library method.

Builtin JSON decoder:

`>>> data = races.json()`

Standard json loads() function:

`>>> data = json.loads(races.text)`

Both return the same result:

```
{'1': {'shortname': 'QAT', 'title': 'Grand Prix of Qatar', 'circuit': 'Losail International Circuit', 'sequence': '1', 'url': '/en/ajax/results/selector/2017/QAT'}, '2': {'shortname': 'ARG', 'title': 'Gran Premio Motul de la República Argentina', 'circuit': 'Termas de Río Hondo', 'sequence': '2', 'url': '/en/ajax/results/selector/2017/ARG'}, '3': {'shortname': 'AME', 'title': 'Red Bull Grand Prix of The Americas', 'circuit': 'Circuit Of The Americas', 'sequence': '3', 'url': '/en/ajax/results/selector/2017/AME'}, '4': {'shortname': 'SPA', 'title': 'Gran Premio Red Bull de España', 'circuit': 'Circuito de Jerez', 'sequence': '4', 'url': '/en/ajax/results/selector/2017/SPA'}, '5': {'shortname': 'FRA', 'title': 'HJC Helmets Grand Prix de France', 'circuit': 'Le Mans', 'sequence': '5', 'url': '/en/ajax/results/selector/2017/FRA'}, '6': {'shortname': 'ITA', 'title': "Gran Premio d'Italia Oakley", 'circuit': 'Autodromo del Mugello', 'sequence': '6', 'url': '/en/ajax/results/selector/2017/ITA'}, '7': {'shortname': 'CAT', 'title': 'Gran Premi Monster Energy de Catalunya', 'circuit': 'Circuit de Barcelona-Catalunya', 'sequence': '7', 'url': '/en/ajax/results/selector/2017/CAT'}, '8': {'shortname': 'NED', 'title': 'Motul TT Assen', 'circuit': 'TT Circuit Assen', 'sequence': '8', 'url': '/en/ajax/results/selector/2017/NED'}, '9': {'shortname': 'GER', 'title': 'GoPro Motorrad Grand Prix Deutschland', 'circuit': 'Sachsenring', 'sequence': '9', 'url': '/en/ajax/results/selector/2017/GER'}, '10': {'shortname': 'CZE', 'title': 'Monster Energy Grand Prix České republiky', 'circuit': 'Automotodrom Brno', 'sequence': '10', 'url': '/en/ajax/results/selector/2017/CZE'}, '11': {'shortname': 'AUT', 'title': 'NeroGiardini Motorrad Grand Prix von Österreich', 'circuit': 'Red Bull Ring – Spielberg', 'sequence': '11', 'url': '/en/ajax/results/selector/2017/AUT'}, '12': {'shortname': 'GBR', 'title': 'Octo British Grand Prix', 'circuit': 'Silverstone Circuit', 'sequence': '12', 'url': '/en/ajax/results/selector/2017/GBR'}, '13': {'shortname': 'RSM', 'title': 'Tribul Mastercard GP S.Marino e Riviera di Rimini', 'circuit': 'Misano World Circuit Marco Simoncelli', 'sequence': '13', 'url': '/en/ajax/results/selector/2017/RSM'}, '14': {'shortname': 'ARA', 'title': 'Gran Premio Movistar de Aragón', 'circuit': 'MotorLand Aragón', 'sequence': '14', 'url': '/en/ajax/results/selector/2017/ARA'}, '15': {'shortname': 'JPN', 'title': 'Motul Grand Prix of Japan', 'circuit': 'Twin Ring Motegi', 'sequence': '15', 'url': '/en/ajax/results/selector/2017/JPN'}, '16': {'shortname': 'AUS', 'title': 'Michelin® Australian Motorcycle Grand Prix', 'circuit': 'Phillip Island', 'sequence': '16', 'url': '/en/ajax/results/selector/2017/AUS'}, '17': {'shortname': 'MAL', 'title': 'Shell Malaysia Motorcycle Grand Prix', 'circuit': 'Sepang International Circuit', 'sequence': '17', 'url': '/en/ajax/results/selector/2017/MAL'}, '18': {'shortname': 'VAL', 'title': 'Gran Premio Motul de la Comunitat Valenciana', 'circuit': 'Circuit Ricardo Tormo', 'sequence': '18', 'url': '/en/ajax/results/selector/2017/VAL'}}
```

## Extract data from dictionary

Once we have the data in a python dictionary, extracting data from it is fairly easy.
Values can be accessed from the dictionary by it's key.

With `>>> list(data.keys())`, we can list the keys of our dictionary:

`['1', '2', '3', '4', '5', '6', '7', '8', '9', '10', '11', '12', '13', '14', '15', '16', '17', '18']`

As you can see, the keys correspond to the number of races scheduled for the 2017 MotoGP season.

We can access each key's corresponding values by using square bracket notation:

`>>> data['1'], data['2'], data['3'], ..., data['18']`

We can loop through the dictionary using the `.items()` method to retrieve keys and corresponding values simultaneously.

```
>>> for k, v in data.items():
    print(k, v)

    
1 {'shortname': 'QAT', 'title': 'Grand Prix of Qatar', 'circuit': 'Losail International Circuit', 'sequence': '1', 'url': '/en/ajax/results/selector/2017/QAT'}
2 {'shortname': 'ARG', 'title': 'Gran Premio Motul de la República Argentina', 'circuit': 'Termas de Río Hondo', 'sequence': '2', 'url': '/en/ajax/results/selector/2017/ARG'}
3 {'shortname': 'AME', 'title': 'Red Bull Grand Prix of The Americas', 'circuit': 'Circuit Of The Americas', 'sequence': '3', 'url': '/en/ajax/results/selector/2017/AME'}
4 {'shortname': 'SPA', 'title': 'Gran Premio Red Bull de España', 'circuit': 'Circuito de Jerez', 'sequence': '4', 'url': '/en/ajax/results/selector/2017/SPA'}
5 {'shortname': 'FRA', 'title': 'HJC Helmets Grand Prix de France', 'circuit': 'Le Mans', 'sequence': '5', 'url': '/en/ajax/results/selector/2017/FRA'}
6 {'shortname': 'ITA', 'title': "Gran Premio d'Italia Oakley", 'circuit': 'Autodromo del Mugello', 'sequence': '6', 'url': '/en/ajax/results/selector/2017/ITA'}
7 {'shortname': 'CAT', 'title': 'Gran Premi Monster Energy de Catalunya', 'circuit': 'Circuit de Barcelona-Catalunya', 'sequence': '7', 'url': '/en/ajax/results/selector/2017/CAT'}
8 {'shortname': 'NED', 'title': 'Motul TT Assen', 'circuit': 'TT Circuit Assen', 'sequence': '8', 'url': '/en/ajax/results/selector/2017/NED'}
9 {'shortname': 'GER', 'title': 'GoPro Motorrad Grand Prix Deutschland', 'circuit': 'Sachsenring', 'sequence': '9', 'url': '/en/ajax/results/selector/2017/GER'}
10 {'shortname': 'CZE', 'title': 'Monster Energy Grand Prix České republiky', 'circuit': 'Automotodrom Brno', 'sequence': '10', 'url': '/en/ajax/results/selector/2017/CZE'}
11 {'shortname': 'AUT', 'title': 'NeroGiardini Motorrad Grand Prix von Österreich', 'circuit': 'Red Bull Ring – Spielberg', 'sequence': '11', 'url': '/en/ajax/results/selector/2017/AUT'}
12 {'shortname': 'GBR', 'title': 'Octo British Grand Prix', 'circuit': 'Silverstone Circuit', 'sequence': '12', 'url': '/en/ajax/results/selector/2017/GBR'}
13 {'shortname': 'RSM', 'title': 'Tribul Mastercard GP S.Marino e Riviera di Rimini', 'circuit': 'Misano World Circuit Marco Simoncelli', 'sequence': '13', 'url': '/en/ajax/results/selector/2017/RSM'}
14 {'shortname': 'ARA', 'title': 'Gran Premio Movistar de Aragón', 'circuit': 'MotorLand Aragón', 'sequence': '14', 'url': '/en/ajax/results/selector/2017/ARA'}
15 {'shortname': 'JPN', 'title': 'Motul Grand Prix of Japan', 'circuit': 'Twin Ring Motegi', 'sequence': '15', 'url': '/en/ajax/results/selector/2017/JPN'}
16 {'shortname': 'AUS', 'title': 'Michelin® Australian Motorcycle Grand Prix', 'circuit': 'Phillip Island', 'sequence': '16', 'url': '/en/ajax/results/selector/2017/AUS'}
17 {'shortname': 'MAL', 'title': 'Shell Malaysia Motorcycle Grand Prix', 'circuit': 'Sepang International Circuit', 'sequence': '17', 'url': '/en/ajax/results/selector/2017/MAL'}
18 {'shortname': 'VAL', 'title': 'Gran Premio Motul de la Comunitat Valenciana', 'circuit': 'Circuit Ricardo Tormo', 'sequence': '18', 'url': '/en/ajax/results/selector/2017/VAL'}
```

You may notice that the values returned are structured in yet dictionary.
Accesing the values can be done by using square bracket notation like we've done previously.

```
>>> for k, v in data.items():
	print(k, v['shortname'], v['title']+' at '+v['circuit'])

	
1 QAT Grand Prix of Qatar at Losail International Circuit
2 ARG Gran Premio Motul de la República Argentina at Termas de Río Hondo
3 AME Red Bull Grand Prix of The Americas at Circuit Of The Americas
4 SPA Gran Premio Red Bull de España at Circuito de Jerez
5 FRA HJC Helmets Grand Prix de France at Le Mans
6 ITA Gran Premio d'Italia Oakley at Autodromo del Mugello
7 CAT Gran Premi Monster Energy de Catalunya at Circuit de Barcelona-Catalunya
8 NED Motul TT Assen at TT Circuit Assen
9 GER GoPro Motorrad Grand Prix Deutschland at Sachsenring
10 CZE Monster Energy Grand Prix České republiky at Automotodrom Brno
11 AUT NeroGiardini Motorrad Grand Prix von Österreich at Red Bull Ring – Spielberg
12 GBR Octo British Grand Prix at Silverstone Circuit
13 RSM Tribul Mastercard GP S.Marino e Riviera di Rimini at Misano World Circuit Marco Simoncelli
14 ARA Gran Premio Movistar de Aragón at MotorLand Aragón
15 JPN Motul Grand Prix of Japan at Twin Ring Motegi
16 AUS Michelin® Australian Motorcycle Grand Prix at Phillip Island
17 MAL Shell Malaysia Motorcycle Grand Prix at Sepang International Circuit
18 VAL Gran Premio Motul de la Comunitat Valenciana at Circuit Ricardo Tormo
```

There we go, we now know how to get the races for a single MotoGP season!
We can apply what we've learned to retrieve the entire race schedule from the inception of the sport in 1949.

In the next part I will go over how I imported the data we've gathered into a database.
