# Simple Sega-vs-Nintendo NetLogo simulation

The project was built in NetLogo for the TEU00522-202324 Systems the Science of Everything at TCD by group 9

The system uses NetLogos setup and go functions combined with a few custom functions the achive the desired market symulation.

## Setup
Upon startup the create-advertisement-patches sets up the advertisment "boards" randomly in the simulation space. The number of these "boards" is based on the variables set by the user using the advertisement-for-company-a and advertisement-for-company-b sliders and are assigned a company and the responding color.

Then the add-consumers spaens the turtles that will sereve as our starting market based on the num-of-agents slider. Initially all customers are grey and are affiliated with company 3 representing the rest of the market.

It then finally reset-ticks and initializes the market-increase-counter to 0 inpreperation to running the simulation.

## Global variables
%other-company: stores the market share percentege for the other company group for graphing.

%company-a: stores the market share percentege for company-a, in the case of dynamic simulation Nintendo for graphing.

%company-b: stores the market share percentege for company-b, in the case of dynamic simulation Sega for graphing.

market-increase-counter: counter that keeps track of ticks for the market increase technicaly DEPRECATED however it allows tuning for slower progression

no_customers: Used to show the number of active customers on a dashboard monitor.

## GO
The main go finction houses the operations of the model.

The move function randomly moves the customers around allowing them to encounter other customers and the marketing spots.

The no_customers variable is updated for use in othe rfunctions

We then run the two adoption functions:

* adoption-from-advertisement
  For every customer we check if they are in aposition where they can interact with a advertisment       "board". If a customer can "view" the ad the we run the adoption rate calculations and see if the   customer will adopt the product or not.
* adoption-from-wom
  For every customer we check if they are interaction with any customer that adopted the products     different from theirs. If they are in interaction range they will atempt to convince the other user to switch to the product they adopted using a similar adoption probability calculation as in the advertisment version. The probability is then rolled on and the customer eighter adopts the recomended   product or not. Customers of neighter companies will not try to convince the adopters of company 1 or 2  to switch away.

Next the exit-market function causes some of the customers that adopted company 1 or 2 to return to the other company pool. THe number of customers departing is related to the decay variable based on which a decay probability is calculated and each customer that already adopted a company roolls on it to see if they switch back to other compnay.

Next we update the global variables which entails the calculation of the 3 market shares and storing them for graphing. The updated variables are:
*%other-company
*%company-a
*%company-b

Next market-growth function is called this function incraments the market-increase-counter varaiable by 1 and serves as a wraper for the increase-market witch is only called every 100 ticks.

The increase-market function then increases the market proportionatly to its size of the existing market while also ensuring the market only grows to 250 customers at most, this was done to prevent runaways, lag and the simulation space becoming a mess.

Finally if the dynamic_consol_pairs variable is set to yes the we call the various console pairing funtions that only run ath the appropriate tick counts. These functions update the price, quality for both companies representing the new product entering the market. In certain functions we also manipulate the decay variable to represent growth of other comanies in the markt, in this case Sony and Microsoft.
The console pairing functions are:
* nes_vs_master_sys
* super_nes_vs_genesis
* saturn_vs_N64
* dreamcast_vs_game_cube

Finally if the program is active the simulation will stop on its own at a point representing Segas Exit from the market and the end of the console war.

NOTE: If the dynamic program is inactive the simulation will continue on.

Finally the ticks are incramented depending on the dynamic_consol_pairs setting and the go loop starts from the beginning.





