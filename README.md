# challonge-elo-nodejs

Get player rankings and elo from challonge tournaments.

## Installation

    npm install --save challonge-elo-nodejs

## Usage

```js
const challongeElo = require('challonge-elo-nodejs');

const config = {
  tournaments: [
    {
      api_key: 'my_challonge_api_key',
      subdomain: 'roaeurope',
      tournament_urls: ['untamed6']
    }
  ],
  elo_multiplier: 2
};

challongeElo.getStats(config).then((stats) => {
  ...
});
```

[View the stats object](stats-example.json)

## API

### challongeElo.getStats(config)

#### config

##### tournaments

Type: `array` of `tournament`

##### tournament

###### api_key

Type: `string`

Your challonge api key, you can get it [here](https://challonge.com/settings/developer).

###### subdomain

Type: `string`

The subdomain of the organization.

e.g. for [http://roaeurope.challonge.com](http://roaeurope.challonge.com) : 'roaeurope'

###### tournament_urls

Type: `array` of `string`

The path of each tournament, at the end of the tournament url. They don't need to be sorted.

e.g. for [http://roaeurope.challonge.com/untamed6](http://roaeurope.challonge.com/untamed6) : 'untamed6'

##### elo_multiplier

Type: `number`

Defaults to 1

The elo [K-factor](https://en.wikipedia.org/wiki/Elo_rating_system#Most_accurate_K-factor) will be multiplied by this number.

#### stats

The method returns a promise that resolves to player stats.

##### players

Type: `array` of `player`.

An array of players with their infos and rankings. Sorted by rank (#1 first).

##### player

###### rank

Type: `number`.

###### elo

Type: `number`.

###### wins

Type: `number`.

###### losses

Type: `number`.

###### total

Type: `number`.

###### winrate

Type: `string`.

###### history

Type: `array` of `match`.

#### match

###### vs

Type: `string`.

The name of the opponent.

###### result

Type: `string`.

The result, `win` or `lose`

###### delta

Type: `string`.

The gain/loss of elo.

###### previous_elo

Type: `number`.

The elo before the match.

###### current_elo

Type: `number`.

The elo after the match

#### tournaments

Type: `array` of `tournament info`.

Tournament infos, sorted by date (most recent first).

#### tournament info

##### name

Type: `string`.

The full name of the tournament on challonge.

##### url

Type: `string`.

The full url of the tournament on challonge.
