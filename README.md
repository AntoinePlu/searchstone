# [Searchstone.io](http://searchstone.io)

![Searchstone](https://cdn-images-1.medium.com/max/2000/1*TDiE4_ANWjtekDNZmisj-g.png)

[Searchstone.io](http://searchstone.io) is an open source search engine for the Heartstone card playing video game.
It relies on [Algolia](https://community.algolia.com/?utm_medium=link&utm_source=github&utm_campaign=searchstone) API for the search and [instantsearch.js](https://community.algolia.com/instantsearch.js/?utm_medium=link&utm_source=githubm&utm_campaign=searchstone) for the UI.

I've published an article on Medium that explain a bit more the project:
[A painstakingly crafted search for Hearthstone](https://medium.com/@Kevin_Granger/a-painstakingly-crafted-search-for-hearthstone-c21b3fa4223c)

## Features
- Search as-you-type experience
- Full-text search in name, description and attributes
- Smart Highlighting
- Multi-language support
- Typo tolerance
- List and grid views
- Refinement on every attributes (Set, Race, Type, Mana, Class, Mechanics, Attack, Health)
- Golden animations cards
- Responsive Design

## Development

### Run the website
```shell
$> yarn install
$> gulp dev
```

### Deploy

```shell
$> NODE_ENV=production gulp deploy
```

### Extension Release Update

#### Config API keys

- edit 'config.json', add your Algolia and Cloudinary credentials (App ID/ API key).

#### Extract pics

- First, update your game to latest version.
- The following commands will install dependencies in a virtual environment:
  ```shell
  $> python3 -m venv myenv
  $> source myenv/bin/activate
  $> pip install --upgrade pip setuptools wheel
  $> pip install unitypack decrunch
  $> pip install lz4 hearthstone unitypack pillow
  ```
- Now, download and run HearthSim's extract script:
  ```shell
  $> git clone https://github.com/HearthSim/HearthstoneJSON.git
  $> cd HearthstoneJSON
  $> python ./generate_card_textures.py --outdir=textures/ /Applications/Hearthstone/Data/OSX/card*.unity3d //or whatever is your game directory
  $> deactivate
  ```
- put all the 512px jpg in the import/art/ folder
- run script gulp cloudinary

#### Update records in Algolia Index

- Select the latest version here https://api.hearthstonejson.com/v1/
- Download card collectible in 'all' languages https://api.hearthstonejson.com/v1/20970/all/cards.collectible.json
- Put the file in import/in
- Run import.js script:
  ```shell
  $> node import
  ```
- upload import/out/algolia-hearthstone.json manually to Algolia (do not use the gulp script, setup is outdated)

### Script update
- look at potential changes on https://hearthstonejson.com/
- update variables set (ie. "ICECROWN": "Knight of the Frozen Throne"), setID (ie. "ICECROWN": 11) and map (ie. "OVERLOAD": "Overload")

### Algolia instantSearch.js configuration
- edit src/js/algolia-instantsearch-conf.js
- update set (ie: ICECROWN), setFull (ie. ICECROWN : "Knight of the Frozen Throne")

### UI

### Sunwell (card generator lib)
I'm running a modified version of the original lib, mostly some perf adjustments because i'm not using its text rendering.
You need to add the image background and other card elements (like premium cards in Knight of the Frozen Throne). Check the updates on the original project. => https://github.com/HearthSim/Sunwell


### Sitemap
- run gulp sitemap (todo: add to deploy)

### Top Decks

### Golden Cards
