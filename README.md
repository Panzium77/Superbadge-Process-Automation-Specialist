# Superbadge-Process-Automation-Specialist



I started this Superbadge in the usual way, by printing this instructions plus the slides and transcripts of the videos.  It is highly recommended to print the video transcripts, because there are a multitude of brief instructions that are easy to overlook while watching.  I also had to keep the volume on my laptop off while doing the challenge- just in case mom was listening in over the baby monitor.  If you are a new Trailhead Baby fan, all you need to know is that I'm a regular baby by day but a daring Trailblazer by night.  Mom is not aware of my nocturnal computing, so I keep the noise to a minimum, and she assumes that I am slumbering away. 

Stage 1.

Step 1 : Create a new Trailhead Playground for the Superbadge and customize the name for easy reference.

Step 2 : Install the managed package. [https://login.salesforce.com/packaging/installPackage.apexp?p0=04t46000001Zch4]

Step 3 : Create validation rule on lead object. 
Name ==> State Validation rule
Formula ==> AND(!ISBLANK( State ), LEN( State ) != 2)

Step 4 : Create 2 queue 
	a) Rainbow Sales 
	b) Assembly System Sales
	
Step 5: create assignment rule on lead
The Rainbow sales team should be handling all the leads that come from the web
other leads come from our partners and from lists that we buy--all those leads are potential buyers of our assembly systems

Check challenge- 500 points

Stage 2

Step 1: On Account object create validation rule so that correct US address can enter into the system

validation rule name ==> country rule for billing add
formula ==>
NOT( 
	OR ( 
		UPPER(BillingCountry) =='US', 
		UPPER(BillingCountry) =='USA', 
		UPPER(BillingCountry) =='United States', 
		UPPER(BillingCountry) ==''
	) 
)

validation rule name ==> country rule for shipping add
formula ==>

NOT( 
	OR ( 
		UPPER(ShippingCountry) =='US', 
		UPPER(ShippingCountry) =='USA', 
		UPPER(ShippingCountry) =='United States', 
		UPPER(ShippingCountry) ==''
	) 
)


validation rule Name ==> State Validation rule for billing add
Formula ==> AND(!ISBLANK( BillingCountry ), LEN(BillingCountry) != 2)


validation rule Name ==> State Validation rule for shipping add
Formula ==> AND(!ISBLANK( ShippingCountry ), LEN(ShippingCountry) != 2)

Step 2: Create one more validation rule so nobody can chage account name if type is customer direct or channel

Name ==> Customer_Direct_or_Channel
Formula==>
OR(
 ISPICKVAL( Type , 'Customer - Direct') ,
 ISPICKVAL( Type , 'Customer - Channel') 
)

Step 3: Create Fields on account 
on the account detail they should be able to see the number of deals, number of won deals, when the last deal was won, what our win percentage is, and the total amount of deals we won.
a) Number of deals=> 
Label = Number of deals
type = rollup summary ( on opportunity function count)

b) Number of won deals =>
Label = Number of won deals
type = rollup summary ( on opportunity function count criteria- stage=close won)

c) Amount of won deals
Label = Number of won deals
type = rollup summary ( on opportunity function sum aggreate field ammount criteria- stage=close won)

d)Last won deal date
Label = Last won deal date
type = rollup summary ( on opportunity function Max aggreate field-close date criteria- stage=close won)

e)Deal win percent
label - Deal win percent
type - formula (return type - percentage )
Number_of_won_deals__c /  Number_of_deals__c 

f)Call for Service
label-Call for Service
type - formula (return type - text )
IF(OR(TODAY() - 730 > Last_Won_Deal_Date__c,TODAY() + 730 < Last_Won_Deal_Date__c) ,'Yes','No')

Stage 3========

step 1: create object robot setup
label - Robot Setup
AutoNumber field - ROBOT SETUP-{0000}

Step 2: create fields

a)Date
label -Date
type -Date

b)Notes
label -Notes
type - text

c)Day of the Week
label -Day of the Week
type - formula (return type - text)
CASE(
MOD(Date__c - DATE(1900, 1, 7), 7), 
0, "Sunday", 
1, "Monday", 
2, "Tuesday", 
3, "Wednesday", 
4, "Thursday", 
5, "Friday", 
6, "Saturday", "Error")

step 3:
create master detail relationship with opportunity


Stage 4====================
