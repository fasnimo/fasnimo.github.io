---
layout: post
title:      "CLI_PROJECT_Rene"
date:       2019-08-11 13:11:28 +0000
permalink:  cli_project_rene
---


Welcome, everyone!

This project is centered around finding the best airport restaurants in America and provide links to there sites. The list of names is 1-20 and the links are embedded with the names. The plan for this project was to be concise and to have a few responses that would achieve some inputs using an “if-else” controller. The website is full of complicated nesting and hidden tags behind ads which made this project both challenging and enjoyable, and I would do it all again because I know it has more potential than I initially had planned for. 

After I had implemented my bundle install an created a name for my repository in Github I began creating the folders “Airport.rb, Scraper.rb, and CLI.rb”. I overlooked my “Environment.rb” and added a “Run” to my “Bin-folder”. The first folder I built into was the Sracper.rb because this is where all of the data I will be working with comes from. Inside of the scraper there is a BASE_URL= with an https: URL because it has to scrape targeted data from this website. Then because I will be focusing on the use of an array I defined an scraper_index that will handle the data I want to scrape. Last to be defined was the scraper_list, which was made to house the list form Airport.rb of the data that was stored, they work together. 

When I made my Airport.rb I saw that I needed to initialize what I wanted which was the :name, and :url_last seen in my attr_accessor. This creates a reader and writer so that an instance method doesn’t need to be made to create one. Next, the initialize method makes those attributes upon creation and then gives them optional nil in case it’s not specified. The @@all is a class variable that I started because it has to be stored in order for the list to be read by my Scraper/CLI.rb(s). The next step for @@all will be to shovel “<<” the class Airport and “all” of its methods into one class method that can be used in other classes such as CLI/Scaper.rb.

The next two definitions are self.all and self.new_list, the names of these are self-explanatory but the methods inside them need some work. The self.all contains an @@all which like the attr_accessor reads all of the written data, well @@all will receive and return what has been stored in it via the shovel “<<”. Without it, the return of the @@all will be nil because you will not have an output of what's been stored. The self.new_list retains the data scraped from the website and filters through it to get what I want. In this case, I will grab the name and link provided that will return all of the information provided bases on the user's input. This method is the most important because it determines what the CLI/Scraper will need. The self in the new list refers to the class Airport which then refers to the @@all << self so that “.all” will have everything from that class. Then the self.new will start upon creation of the application process and store the data between the (). 

In this case there are blocks of code inside the () to serve for an easy transition of the data I want to transfer into the class .self. The first block “l.css(‘h4’).collect{|s| s.css(‘strong’).text.strip” takes what is presented by the scraped date (“.entry-content .listicle-page”) and only receives the h4 type case and collects the data between it the h4 and strong, then it specifies it as a text and strips the brackets. Last it the (l.css(‘h4’).attribute(‘href’)), this line of code targets the h4 and scrapes the attribute that this coupled with the href, which it the link. This method .new_list is then stored in the Scraper method list_airport so that when the CLI runs it commands it will have the data information available. Inside of my CLI is the BASE_URL which it refers to when retrieving from scrape, and the method “run” is defined. This method receives all necessary calls from the Scaper class so that the methods within scraper will run. The fly method is also called because it is my initial start to all of the loops present in my CLI, and a puts for a greeting.

As for the “fly” method, I start with instructions of puts then gets.strip.downcase will receive the inputs provided into strings that will initiate a number given by the index inside of the “scrape_index” method. If the number command is to see the first half of the list then the selection will give you the first 1-10, if last then 11-20. Then if the user is done they would type “Y” and exit. The code below stores the “the_airport”, and “r_info”. Although there is a list stored in my Airport class, I have a “the_airport” method that tells the list how to print it. So, if the input is comparable to 1 then put name and URL to the user for the first half of the list “else” the print response and then the last half of the list. It does this by iterating over the given list with Airport.first(10)/Airport.last(10) because I am returning objects inside of string interpolators “#{}”. 

Finally, the r_info will resond to the defined doc, name, and url_last to give me infromation that the user wants. This is done by calling the number connected to some responses given through prompts, so whatever you chose the methods will be invoked. From beginning to end the project has shown me how parent-child relationships work and learning how to get them to corroperate was worth all the hours. 

Kind regards, Rene Cocom



