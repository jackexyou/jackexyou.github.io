---
layout: post
title:  "CLI Data Gem Project - OLG Lotto"
date:   2017-06-27 20:43:38 +0000
---


I have worked at a convenience store forover 10 years and one of the biggest sells are lottery tickets. Every morning I'd put out sheets with the winning numbers and prize categories on them, so I thought to myself "Why not scrape their website for numbers?" With that in mind I headed to http://www.olg.ca/index.jsp to see what I could do. Check out 
https://github.com/jackexyou/lotto_cli_gem for my full code.

---

To start off I designed the Game class:
```
class LottoCliGem::Game
  attr_accessor :name, :winning_numbers, :bonus

  @@all = []

  def initialize(name, winning_numbers)
  end

  def self.create_game(name, winning_numbers)
  end

  def self.all
  end

  def self.find_game(name)
  end

end

```

There are several different types of lottery tickets you can get, but most of them share a `:name`, `:winning_numbers`, and `:bonus` number. 

I created a class array `@@all` all to store all the games after they're created so I repeatedly access the winning numbers through `self.all`. 

`self.create_game` is used to add all the game instances into the `@@all` array after the scraper gets all the game data from the website. 

`self.find_game` is used for CLI to access the scraped game data, specfically the 

---

Next, I moved on to the scraper class so I could see what data I could pull:

```
class LottoCliGem::Scraper

  def get_games
  end


  def get_winning_number(game_url)
  end

  def scrape_all(game_urls)
  end

end
```

`get_games` is used to scrape the urls of individual game page where the winning numbers are located. It looks through the navbar of the OLG website and picks out the url to each game page. It outputs the list in an array.

`get_winning_number` scrapes for the winning numbers on the page and returns them as an array.

`scrape_all` takes in a list of arrays (the one `get_games` produces) and iterates through each url and finding the winning numbers from each link with `get_winning_number`

---
Next up is my ticket class which is modeled after a lottery ticket: 

```
class LottoCliGem::Ticket
  attr_accessor :game, :numbers

  @@all = []

  def initialize(game)
  end

  def add_number(input)
  end

  def self.all
  end

  def self.create(game_name)
  end

  def matches
  end
end

```

Each ticket is defined by a Game instance `:game` and an array of `:numbers`

`add_number` takes in a number and places it in an instance array keeps track of the numbers of an individual ticket
`self.all` returns the `@@all` array that keeps track of all `Ticket` instances
`self.create` custom initialize method that saves all instances to `@@all` after they're created
`matches` returns the matching numbers of a ticket when compared to the winning numbers of it's `Game`

---

Lastly the CLI class attempts to put everything together with a user interface.

```
class LottoCliGem::CLI
  
  def call
  end

  def list_all_games
  end

  def winning_numbers(input)
  end

  def first_prompt
  end

  def winning_number_prompt

  end

  def add_ticket_prompt
  end

  def add_numbers_prompt(ticket)
  end

  def matching_numbers_prompt
  end
	
end

```

`call` is the method that encapsulates everything and is the only method called in the bin executable. It initializes the scraper to populate the `Game` data. It then starts the user interface by calling `first prompt`

`list_all_games` is a helper method that formats the data sent in from calling `Game.all.names`
`winning numbers` is a help method that converts user input and returns the correct set of winning numbers.
`first prompt` is the initial menu that appears giving 3 choices: 
1. See winning numbers: `winning_number_prompt` brings up the menu where you choose what game's winning numbers you'd like to see
2. Add your own numbers: `add_ticket_prompt` asks you for the game name of your ticket and then brings up `add_numbers_prompt(ticket)` which lets you add all the numbers on your ticket
3. Check if your numbers matched: `matching_numbers_prompt` then iterates through each ticket you added and compares them to the winning numbers. It then returns all the numbers that were matched on each ticket.

---

Overall this project really helped me apply the skills I've learned in the last couple of months and with more projects to come, I'm definitely looking forward to becoming a full fledged developer.




