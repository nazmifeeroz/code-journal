# 100 Days Of Code - Log

### Day 1: 1 January 2018 (AngularJS)

**Today's Progress**: Fixed issues with the filters in my angularJS app.

**Thoughts:** I was told not to learn angularJS but for the sake of a job, I'm learning angularJS. plus it is version 1! but honestly angularJS is much more easier than reactJS. Today done all the CRUD functions in angularJS. 

I used [reload](https://www.npmjs.com/package/reload) as my localhost server. it automatically reloads the webpage when i save my codes. Very useful!

**Link to work:** [Classifieds App](https://github.com/nazmifeeroz/angular-classifieds)


### Day 2: 2 January 2018 (AngularJS)

**Today's Progress**: Learn a new technique using UI-Router.

**Thoughts:** Had many problems making the ui-router works. Turns out that the name has changed and the tutorial was using an outdated plugin. Initially was angular-ui-router, now its @uirouter. Lots of troubleshooting and forgot to add the stateProvider!

**Link to work:** [Classifieds App](https://github.com/nazmifeeroz/angular-classifieds)

### Day 3: 3 January 2018 (Ruby on Rails)

**Today's Progress**:

Started a new freelance project. Using `Time` and `SecureRandom.hex()` to generate tracking IDs.

```ruby
time = Time.new
puts "Current Time : " + time.inspect
 
puts time.year    # => this will show the year of the date
 
puts time.month   # => will show month of the date
 
puts time.day     # => will show day of the date
 
puts time.wday    # => will show the day of week: 0 = Sunday and go on
 
puts time.yday    # => will show the day of the year (365 days)
 
puts time.hour    # => will show 24 hours of clock 
 
puts time.min     # => total min of hour
 
puts time.sec     # => total sec of hour
 
puts time.usec    # => this will show the microseconds of that hour
 
puts time.zone    # => this will show time zone (UTC) (GMT)
```

Also learnt using Stripe:
```ruby
# gemfile
gem 'stripe'

#------------------------------------------------------------

# config/initializers/stripe.rb
Rails.configuration.stripe = {
  :publishable_key => ENV['PUBLISHABLE_KEY'],
  :secret_key      => ENV['SECRET_KEY']
}

Stripe.api_key = Rails.configuration.stripe[:secret_key]

#------------------------------------------------------------

# Charges controller 
class ChargesController < ApplicationController

  def new
  end
  
  def create
    # Amount in cents
    @amount = 500
  
    customer = Stripe::Customer.create(
      :email => params[:stripeEmail],
      :source  => params[:stripeToken]
    )
  
    charge = Stripe::Charge.create(
      :customer    => customer.id,
      :amount      => @amount,
      :description => 'Rails Stripe customer',
      :currency    => 'usd'
    )
  
  rescue Stripe::CardError => e
    flash[:error] = e.message
    redirect_to new_charge_path
  end
  
end

```