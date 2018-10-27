### TablePrint
---
.rb
https://github.com/arches/table_print
.py


```sh
CreditCard.all 

gem install table_print
bundle install

irb
rails c

```


```sql
tp Book.all
tp User.limit(30), :include => :yearly_income, :except => :hourly_rate
tp User.limit(30), :address, 'city', 'state', :zip
tp Author.limit(3), "name", "books.title", "books.photos.caption"
tp User.all, :email => {:width => 12}
tp User.all, :id, {:email => {:width => 12}}, :age

tp User.all, :active => {:display_method => :active_in_the_past_siz_months}

tp User.all, :email, :monthly_payment, yearly_payment: lambda{|u| u.monthly_payment * 12}
tp User.all, :yearly_payment => {:display_method => lambda{|u| u.monthly_payment * 12}, :width => 10}
tp User.all, :email, { daily_payment: lambda {|u| u.monthly_payment / 30} }, :monthly_payment, { yearly_payment: lambda { |u| u.monthly_payment * 12} }

# >
tp User.first
tp User.first, :except => :email
tp User.first, first_name

tp.clear User

tp.set User, :id, :email
tp.config_for User

tp.set :max_width, 10
tp.set :time_format, "%Y"
tp.set :capitalize_headers, false

f = File.open("users.txt", "w")
tp.set :io, f
tp User.all
tp.clear :io
tp User.all

tp.set :multibyte, true

```

```ruby
class NoNewlineFormatter
  def format(value)
    value.to_s.gsub(/\r\n/, " ")
  end
end
tp User.all, :bio => {:formatters => [NoNewlineFormatter.new]}

def tp_pre data, options={}
  content_tag :pre, TablePrint::Printer.new(data, options).table_print
end

tp.set :separator, ","

tp.set User, :id, :email

```
