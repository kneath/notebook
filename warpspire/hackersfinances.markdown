Managing your finances - hacker style

In some ways managing your finances can be more of a hassle than your actual job.  If you live in America, you're familiar with the maze that is our Tax Code.  Figuring out how much you make can be pretty damn hard, even if you're getting a steady paycheck from your employer.  Throw in a few freelance contracts, some Google Adsense checks and it's easy to have *no idea* how much money you're actually taking home.  April 15th comes and is a lot like rolling to Vegas... do I win? Do I lose? Wait, where are you towing my car to?

But there's a solution. And I'm going to lay it out for you.  My personal setup includes a few ruby scripts, a couple of spreadsheets, and a few tax returns to use for reference.  Before we begin, I'm going to lay down some **assumptions** -- or rather, **what my situation is**.  I make most of my money through contracting work (income through a sole-proprietorship), and have some miscellaneous income streams -- referral payments, ad payments, etc.

##  First Step: End budget fail

The first step in my plan involves figuring out *just how much money you spend every month*.  First, lay out your known expenses every month in a spreadsheet. 

<div class="figure"><img src="http://share.kyleneath.com/captures/Personal_Finances-20090407-014744.jpg" /></div>

Got it? Alright, now sign up for [Mint](http://mint.com) and figure out what your *real* expenses are.  I'm betting you're going to have a big chunk of money that doesn't seem to be spent on anything in particular, but is *still spent*. That's the "WTF" number in my spreadsheet.

That number? That's your paycheck from now on. (This should be less than you make every month)

## Second Step: Oh God, *how* much is government going to take from me?

As a card-carrying member of the United States, you have the privilege of paying (at least) three taxes out of your paycheck: Federal Income Tax, State Income Tax and Self-Employment Tax.  Each of these are inter-dependent and vary on your income. It's kind of like a Mad Libs puzzle, except when you can't figure it out the government steals all your money.

So I made a ruby script to figure it all out (based on the 2008 tax code):


This code will return the your *highest possible liability*.  It doesn't include any deductions or any of the interdependent effects. It just works on the tax brackets and lets you know the taxes you start off with.  Breathe a sigh of relief knowing that the actual amount will be much less.

This is why I use my past tax forms to figure out how much I've paid in the past.  Using some wishy-washy estimations between the percentage of income I paid in taxes for previous years and the percentage my ruby script comes up with based on my expected income, I come up with a pretty good estimation of what my taxes will look like. Now add a few percent. This is the percent of income you'll be putting aside for taxes.

## Third Step: Create your month-to-month spreadsheet

Alright, so this last spreadsheet has an ominous number of columns -- but I assure you, they all have a purpose. It's going to tell you how rich you are. Let's run down the columns:

* **Total Income** - this is how much money you'll be receiving from contracting, ads, etc in a particular month (not what you invoice, but rather what you will receive).
* **Personal Income** - this is how much you're going to pay yourself for the month. It should be the number from step 1.
* **For Taxes** - automatically calculated based on your tax rate that you calculated in step 2. This is how much you need to be setting aside for taxes that month.
* **For Savings** - automatically calculated based on what's leftover from your income and taxes.
* **Savings Total** - this is the amount of *pure savings* you have in your account (NOT the balance of your savings account)
* **Yearly Income** - automatically calculated estimate of how much you'll make this year based on your previous month's income
* **Tax Man Payments** - this is how much you actually end up sending the tax man for estimated tax payments (hey, you're paying your quarterly taxes as a self-employed individual, right?)
* **Savings Balance** - this is the running *balance* of your savings accounts. It includes your actual savings as well as any tax payments you've deferred.

## The workflow

The last bit is tying all this up into an automated workflow.  It's actually pretty easy for me.  First off, I have two accounts: a checking account at Bank of America, and a high-yield savings account at Emigrant Direct.  All income goes into Emigrant Direct, all expenses come out of Bank of America.  To recap:

* Every single dime of income goes into my savings account
* Once a month, I pay myself a salary from my savings account to my checking account
* Four times a year I pay my estimated tax payments by transferring the money from my savings to my checking, then write a check to the IRS, California, or whoever wants to steal my money for the given quarter.

## Why this workflow rocks

As a contractor I don't necessarily get paid once a month. Sometimes invoices are paid late, sometimes they're paid early.  If you're not careful it can be easy to lose track of how much money you need to be saving to cover next month's expenses.  As you make sure all your income is *savings first* you're protected from late invoices (assuming you've got a savings buffer).

Another benefit is that I get to make money on my tax money (something you W2 chumps know nothing about). For 3 months a year I get to keep the money in my high-yield savings account earning interest for me.

Really, this is all about taking control of your finances. Just because you don't get paid every two weeks from your employer doesn't mean you can't have a steady income stream.  I don't have to worry about late invoices so much anymore, because it doesn't affect me month-to-month.

As a final note, if you've got any credit card debt, feel lost by banks, have any money in a mutual fund, or are picking stocks -- you should pick up [I Will Teach You to be Rich]() -- it's a great book covering the basics of personal finance.