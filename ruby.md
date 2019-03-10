```ruby
Dir["*"].each do |a|
  puts "#{a}:#{File.stat(a).size}"
end
```
